<template>
  <!-- Contêiner fixo principal -->
  <div class="fixed z-[100] transition-all duration-[800ms] ease-[cubic-bezier(0.25,1,0.5,1)] pointer-events-none"
    :style="mascotStyle" :class="{
      'mascot-hero': isHero,
      'mascot-footer': !isHero && scrollMaxGlobal > 0 && currentScroll >= scrollMaxGlobal - 20,
      'mascot-scrolled': !isHero && !(scrollMaxGlobal > 0 && currentScroll >= scrollMaxGlobal - 20)
    }">

    <!-- Texto RPG (Aparece apenas na Hero) -->
    <div
      class="absolute -top-8 md:-top-12 left-1/2 -translate-x-1/2 text-foreground font-bold text-xl md:text-2xl transition-all duration-500 flex items-center justify-center whitespace-nowrap"
      style="font-family: 'Pixelify Sans', cursive; font-weight: 600; letter-spacing: 0.05em;"
      :class="isHero ? 'opacity-100 translate-y-0 scale-100 delay-[600ms]' : 'opacity-0 translate-y-4 scale-75 pointer-events-none blur-sm'">
      Oi!
    </div>

    <!-- Wrapper Perfeito (Arredonda os cantos reais do video sem adicionar fundos falsos) -->
    <div
      class="w-full h-auto rounded-[1.5rem] md:rounded-[2rem] overflow-hidden shadow-2xl relative flex items-center justify-center">
      <video ref="videoRef" src="../assets/video-avatar-kf.mp4" muted playsinline
        class="block w-full h-full object-contain pointer-events-none"></video>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const videoRef = ref(null)
let reqFrame = null

// Rastreamento local da rolagem para atrelar ao CSS e ao Scrub
const currentScroll = ref(0)
const scrollMaxGlobal = ref(0)
const anchorRect = ref(null)

const isHero = computed(() => currentScroll.value < 100)
let hasStartedScrolling = false

const updateAnchor = () => {
  const isMobile = window.innerWidth < 768
  const anchorId = isMobile ? 'mascot-anchor' : 'mascot-anchor-desktop'
  const anchor = document.getElementById(anchorId)
  
  if (anchor) {
    anchorRect.value = anchor.getBoundingClientRect()
  } else {
    anchorRect.value = null
  }
}

const mascotStyle = computed(() => {
  // HERO STATE: Segue a âncora (Mobile ou Desktop)
  if (isHero.value && anchorRect.value) {
    const isMobile = window.innerWidth < 768
    return {
      top: `${anchorRect.value.top}px`,
      left: `${anchorRect.value.left}px`,
      width: `${anchorRect.value.width}px`,
      height: `${anchorRect.value.height}px`,
      padding: isMobile ? '3rem' : '1rem', // Respiro menor no desktop para preencher melhor o grid
      bottom: 'auto',
      right: 'auto',
    }
  }

  // DEFAULT (Scrolled ou Footer)
  const isMobile = window.innerWidth < 768
  return {
    bottom: isMobile ? '1rem' : '2.5rem',
    right: isMobile ? '1rem' : '2.5rem',
    width: isMobile ? '9rem' : '16rem', // w-36(144px) vs w-64(256px)
    height: 'auto',
    top: 'auto',
    left: 'auto',
    padding: '0',
  }
})

const updateVideoTime = () => {
  if (!videoRef.value) return

  updateAnchor() // Atualiza a âncora a cada frame se necessário

  const docHeight = document.documentElement.scrollHeight
  const winHeight = window.innerHeight
  const scrollMax = docHeight - winHeight

  const scrollY = Math.max(0, Math.min(window.scrollY, scrollMax))
  currentScroll.value = scrollY // Alimenta o estado IsHero
  scrollMaxGlobal.value = scrollMax // Alimentar o calculo do Footer

  if (scrollY > 5) {
    if (!hasStartedScrolling) {
      videoRef.value.pause()
      hasStartedScrolling = true
    }
  }

  // Apenas fazemos Scrub se o usuário já engajou com o Scroll
  // Caso contrário, deixamos rodar natural do Play() inicial
  if (hasStartedScrolling) {
    const fraction = scrollMax > 0 ? scrollY / scrollMax : 0
    const duration = videoRef.value.duration || 0

    if (duration > 0) {
      videoRef.value.currentTime = duration * fraction
    }
  }

  reqFrame = requestAnimationFrame(updateVideoTime)
}

onMounted(() => {
  if (videoRef.value) {
    // Dá play assim que carregar
    videoRef.value.play().catch(e => console.log('Autoplay blocked:', e))

    // Escuta o tempo para pausar forçadamente em 0.5 segundos se o uusuário não scrollou
    videoRef.value.addEventListener('timeupdate', () => {
      if (!hasStartedScrolling && videoRef.value.currentTime >= 0.4) {
        videoRef.value.pause()
        videoRef.value.currentTime = 0.4 // Crava visualmente no exato momento
      }
    })

    videoRef.value.addEventListener('loadedmetadata', () => {
      reqFrame = requestAnimationFrame(updateVideoTime)
    })

    if (videoRef.value.readyState >= 1) {
      reqFrame = requestAnimationFrame(updateVideoTime)
    }
  }
})

onUnmounted(() => {
  if (reqFrame) cancelAnimationFrame(reqFrame)
})
</script>

<style scoped>
/* Posição quando rolado para baixo (flutuando no canto inferior direito) */
.mascot-scrolled {
  transform: translate(0, 0) scale(1);
  transform-origin: bottom right;
}

/* Posição ao atingir o Footer (Final da Página) */
.mascot-footer {
  /* MOBILE: Sobe para o enorme espaço vazio ANTES do Footer começar */
  transform: translateX(calc(-50vw + 1rem + 50%)) translateY(-16rem) scale(1.1);
  transform-origin: bottom center;
}

@media (min-width: 768px) {
  .mascot-footer {
    /* No Desktop obedece o canto normal do scrolled para não cobrir nada */
    transform: translate(0, 0) scale(1);
    transform-origin: bottom right;
  }
}

/* Posição ancorada na Hero */
.mascot-hero {
  /* Controlado pelo :style dinâmico (Anchor Tracking) para Mobile e Desktop */
  transform: none; 
}
</style>
