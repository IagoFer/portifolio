<template>
  <div
    :class="[
      'min-h-screen transition-colors duration-500',
      isDark ? 'bg-black text-white' : 'bg-white text-gray-900'
    ]"
  >
    <ThemeToggle :isDark="isDark" :toggleTheme="toggleTheme" />

    <main class="relative">
      <HeroSection :isDark="isDark" />
      <AboutSection :isDark="isDark" />
      <ExperienceSection :isDark="isDark" />
      <ProjectsSection :isDark="isDark" />
    </main>

    <Footer :isDark="isDark" />
  </div>
</template>

<script setup>
import { ref, watch, nextTick } from 'vue'
import AOS from 'aos'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import Footer from './components/Footer.vue'
import ThemeToggle from './components/ThemeToggle.vue'

const isDark = ref(localStorage.getItem('theme') === 'dark' ?? true)

watch(isDark, async (val) => {
  localStorage.setItem('theme', val ? 'dark' : 'light')
  if (val) {
    document.documentElement.classList.add('dark')
  } else {
    document.documentElement.classList.remove('dark')
  }
  await nextTick()
  AOS.refresh()
  // Pequeno truque para forçar reavaliação dos elementos visíveis
  setTimeout(() => {
    window.dispatchEvent(new Event('scroll'))
  }, 100)
})

const toggleTheme = () => {
  isDark.value = !isDark.value
}
</script>