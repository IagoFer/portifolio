<template>
  <section class="relative min-h-screen flex items-center justify-center overflow-hidden">
    <!-- Fundo gradiente -->
    <div
      class="absolute inset-0"
      :class="isDark ? 'bg-gradient-to-br from-purple-900/20 via-black to-blue-900/20' : 'bg-gradient-to-br from-purple-100 via-white to-blue-100'"
    />

    <!-- Elementos animados de fundo (mantidos sem AOS) -->
    <div
      class="absolute top-20 left-10 w-72 h-72 rounded-full blur-3xl"
      :class="isDark ? 'bg-purple-500/10' : 'bg-purple-300/30'"
      style="animation: float 8s infinite ease-in-out"
    />
    <div
      class="absolute bottom-20 right-10 w-96 h-96 rounded-full blur-3xl"
      :class="isDark ? 'bg-blue-500/10' : 'bg-blue-300/30'"
      style="animation: float 10s infinite ease-in-out reverse"
    />

    <div class="relative z-10 max-w-7xl mx-auto px-6 flex flex-col lg:flex-row items-center gap-12">
      <!-- Avatar (sem animação ou com AOS) -->
      <div class="w-full lg:w-1/2 h-[400px] lg:h-[500px]" data-aos="fade-right">
        <Avatar3D />
      </div>

      <!-- Texto -->
      <div class="w-full lg:w-1/2 text-center lg:text-left">
        <p
          class="text-lg mb-2"
          :class="isDark ? 'text-purple-400' : 'text-purple-600'"
          data-aos="fade-up"
          data-aos-delay="100"
        >
          Olá, eu sou
        </p>
        <h1
          class="text-5xl lg:text-7xl font-bold mb-4"
          :class="isDark ? 'text-white' : 'text-gray-900'"
          data-aos="fade-up"
          data-aos-delay="200"
        >
          Iago Fernandes Bastos
        </h1>
        <div
          class="h-1 w-24 bg-gradient-to-r from-purple-500 to-blue-500 mb-6 mx-auto lg:mx-0 origin-left"
          data-aos="zoom-in"
          data-aos-delay="300"
          data-aos-duration="800"
        />
        <p
          class="text-xl lg:text-2xl mb-8"
          :class="isDark ? 'text-gray-300' : 'text-gray-700'"
          data-aos="fade-up"
          data-aos-delay="400"
        >
          Desenvolvedor Full Stack
          <br />
          <span :class="isDark ? 'text-purple-400' : 'text-purple-600'">
            Java • Vue • React • Node
          </span>
        </p>

        <!-- Redes sociais -->
        <div
          class="flex gap-4 justify-center lg:justify-start mb-8"
          data-aos="fade-up"
          data-aos-delay="500"
        >
          <a
            v-for="(social, index) in socialLinks"
            :key="index"
            :href="social.url"
            target="_blank"
            rel="noopener noreferrer"
            class="p-3 rounded-full backdrop-blur-sm transition-colors"
            :class="isDark ? 'bg-white/10 hover:bg-white/20' : 'bg-gray-900/10 hover:bg-gray-900/20'"
            data-aos="zoom-in"
            :data-aos-delay="600 + index * 100"
          >
            <component :is="social.icon" class="w-6 h-6" />
          </a>
        </div>

        <button
          @click="scrollToAbout"
          class="px-8 py-3 rounded-full bg-gradient-to-r from-purple-500 to-blue-500 text-white font-semibold hover:shadow-lg hover:shadow-purple-500/50 transition-shadow"
          data-aos="fade-up"
          data-aos-delay="800"
        >
          Conheça meu trabalho
        </button>
      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 animate-bounce">
      <ArrowDown class="w-6 h-6" :class="isDark ? 'text-white/50' : 'text-gray-900/50'" />
    </div>
  </section>
</template>

<style scoped>
@keyframes float {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(30px, 20px); }
}
</style>

<script setup>
import { Github, Linkedin, Mail, ArrowDown } from 'lucide-vue-next'
import Avatar3D from './Avatar3D.vue'

defineProps({
  isDark: Boolean
})

const socialLinks = [
  { icon: Github, url: 'https://github.com/iagofernandes' },
  { icon: Linkedin, url: 'https://linkedin.com/in/iago-fernandes-bastos' },
  { icon: Mail, url: 'mailto:iagofernandesbastos@gmail.com' }
]

const scrollToAbout = () => {
  document.getElementById('about')?.scrollIntoView({ behavior: 'smooth' })
}
</script>