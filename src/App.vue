<template>
  <!-- Definir bg-background na raiz central para que as seções possam ser bg-transparent e o vídeo não suma -->
  <div class="min-h-screen bg-background transition-colors duration-500 relative overflow-hidden">
    
    <!-- ZOOM PARALLAX BACKGROUND (Avanço/Túnel) restaurado sobre toda a tela -->
    <div class="pointer-events-none fixed inset-0 w-full h-full overflow-hidden -z-40">
         <div class="absolute inset-0 w-full h-full origin-center transition-transform duration-75 ease-out"
              :style="{ transform: `scale(${1 + scrollY * 0.0015})` }">
              
              <!-- Padrão imersivo para dar noção de avanço/recuo de vídeo -->
              <div class="absolute inset-0" style="background-image: repeating-linear-gradient(45deg, var(--border) 0, var(--border) 1px, transparent 1px, transparent 120px); opacity: 0.15;" />
              <div class="absolute inset-0" style="background-image: repeating-linear-gradient(-45deg, var(--border) 0, var(--border) 1px, transparent 1px, transparent 120px); opacity: 0.15;" />
              <div class="absolute top-[20%] left-[20%] w-[40vw] h-[40vw] max-w-[600px] rounded-full bg-foreground/[0.04] blur-[120px]" />
         </div>
    </div>

    <!-- PARALLAX GLOW BLOBS RESTANTES -->
    <div class="pointer-events-none fixed inset-0 -z-40">
       <div class="absolute top-[50%] right-[10%] w-[400px] h-[400px] rounded-full bg-foreground/5 blur-[120px]" 
            :style="{ transform: `translateY(${-scrollY * 0.25}px)` }" />
    </div>

    <!-- GLOBAL SCROLLING VIDEO AVATAR -->
    <VideoAvatar />

    <ThemeToggle :isDark="isDark" :toggleTheme="toggleTheme" />

    <main class="relative z-0">
      <HeroSection :isDark="isDark" />
      <AboutSection :isDark="isDark" />
      <ProjectsSection :isDark="isDark" />
      <ExperienceSection :isDark="isDark" />
    </main>

    <Footer :isDark="isDark" class="relative z-10" />
  </div>
</template>

<script setup>
import { ref, watch, nextTick, onMounted } from 'vue'
import AOS from 'aos'

import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import Footer from './components/Footer.vue'
import ThemeToggle from './components/ThemeToggle.vue'
import VideoAvatar from './components/VideoAvatar.vue'

/*
  DARK MODE DEFAULT
*/
const savedTheme = localStorage.getItem('theme')

const isDark = ref(
  savedTheme ? savedTheme === 'dark' : true
)

/*
  SCROLL PARALLAX TRACKER
*/
const scrollY = ref(0)
const handleScroll = () => {
    scrollY.value = window.scrollY
}

/*
  APPLY THEME ON LOAD (evita flash branco)
*/
onMounted(() => {
  if (isDark.value) {
    document.documentElement.classList.add('dark')
  }
  window.addEventListener('scroll', handleScroll, { passive: true })
})

import { onUnmounted } from 'vue'

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

/*
  WATCH THEME CHANGE
*/
watch(isDark, async (val) => {
  localStorage.setItem('theme', val ? 'dark' : 'light')

  if (val) {
    document.documentElement.classList.add('dark')
  } else {
    document.documentElement.classList.remove('dark')
  }

  await nextTick()
  AOS.refresh()

  setTimeout(() => {
    window.dispatchEvent(new Event('scroll'))
  }, 100)
})

const toggleTheme = () => {
  isDark.value = !isDark.value
}
</script>