<template>
  <section class="relative min-h-[100dvh] flex flex-col w-full md:justify-center">
    <!-- Asymmetric Split Grid Layout -->
    <div
      class="relative z-10 w-full max-w-[1400px] mx-auto px-6 md:px-12 grid grid-cols-1 md:grid-cols-2 gap-12 lg:gap-24 items-center pt-24 md:pt-0">

      <!-- Text Content -->
      <div class="flex flex-col items-start order-2 md:order-1 text-left w-full h-full justify-center">

        <div class="inline-flex overflow-hidden rounded-full border border-border bg-secondary/50 px-3 py-1 mb-6"
          data-aos="fade-up">
          <span class="text-xs font-semibold tracking-wide uppercase text-muted-foreground">
            Disponível para novos projetos
          </span>
        </div>

        <h1 data-aos="fade-up" data-aos-delay="200"
          class="text-4xl md:text-6xl lg:text-7xl font-bold tracking-tighter leading-none mb-6 text-foreground">
          Iago Fernandes Bastos
        </h1>

        <p data-aos="fade-up" data-aos-delay="300"
          class="text-lg md:text-xl text-muted-foreground leading-relaxed max-w-[65ch] mb-8">
          Engenheiro Full Stack focado em arquitetar sistemas escaláveis e desenhar interfaces funcionais que não
          parecem sistemas genéricos.
        </p>

        <!-- ROTATING VALUE -->
        <div data-aos="fade-up" data-aos-delay="400" class="mb-10 w-full relative h-[40px]">
          <Transition name="fade-slide" mode="out-in">
            <p :key="currentPhrase"
              class="text-xl md:text-2xl font-medium tracking-tight text-foreground/80 absolute inset-0">
              {{ currentPhrase }}
            </p>
          </Transition>
        </div>

        <div class="flex flex-wrap gap-4 items-center" data-aos="fade-up" data-aos-delay="500">
          <button @click="scrollToProjects"
            class="px-8 py-3.5 rounded-full bg-primary text-primary-foreground font-semibold hover:bg-primary/90 transition-transform active:scale-[0.98]">
            Explorar trabalhos
          </button>

          <!-- SOCIAL -->
          <div class="flex gap-2">
            <a v-for="(social, index) in socialLinks" :key="index" :href="social.url" target="_blank"
              class="w-12 h-12 flex items-center justify-center rounded-full border border-border bg-background transition-all hover:bg-secondary hover:scale-[1.02] active:scale-[0.98]">
              <component :is="social.icon" class="w-5 h-5 text-foreground" />
            </a>
          </div>
        </div>
      </div>

      <!-- MASCOT ANCHOR (Desktop only) -->
      <div id="mascot-anchor-desktop" class="hidden md:flex items-center justify-center h-full min-h-[400px] relative z-0 order-1 md:order-2">
        <!-- O VideoAvatar global será posicionado sobre este div via JS -->
      </div>
    </div>

    <!-- MASCOT ANCHOR (Mobile only) -->
    <!-- Este div cresce para ocupar todo o espaço vago entre o conteúdo e o final da seção -->
    <div id="mascot-anchor" class="flex-grow md:hidden min-h-[30vh] w-full relative z-0 mt-12"></div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { Github, Linkedin, Mail } from 'lucide-vue-next'
import { WhatsAppIcon } from 'vue3-simple-icons'

defineProps({
  isDark: Boolean
})

/* ===== ROTATING VALUE PROPOSITION ===== */
const phrases = [
  'Construindo sistemas escaláveis.',
  'Liderando times técnicos.',
  'Criando produtos de impacto.'
]

const currentPhrase = ref(phrases[0])
let index = 0
let interval

onMounted(() => {
  interval = setInterval(() => {
    index = (index + 1) % phrases.length
    currentPhrase.value = phrases[index]
  }, 2200)
})

onUnmounted(() => {
  clearInterval(interval)
})

/* ===== SOCIAL ===== */
const socialLinks = [
  { icon: Github, url: 'https://github.com/IagoFer' },
  { icon: Linkedin, url: 'https://linkedin.com/in/iago-fernandes-bastos' },
  { icon: Mail, url: 'mailto:iagofernandesbastos@gmail.com' },
  { icon: WhatsAppIcon, url: 'https://wa.me/5585997900737' }
]

const scrollToProjects = () => {
  document.getElementById('projects')?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<style scoped>
/* TEXT TRANSITION */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all .5s cubic-bezier(0.16, 1, 0.3, 1);
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>