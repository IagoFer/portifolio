<template>
  <section class="relative min-h-screen flex items-center justify-center overflow-hidden">
    <!-- Fundo gradiente -->
    <div
      class="absolute inset-0"
      :class="isDark ? 'bg-gradient-to-br from-purple-900/20 via-black to-blue-900/20' : 'bg-gradient-to-br from-purple-100 via-white to-blue-100'"
    />

    <!-- Elementos animados de fundo -->
    <div
      class="absolute top-20 left-10 w-72 h-72 rounded-full blur-3xl animate-float"
      :class="isDark ? 'bg-purple-500/10' : 'bg-purple-300/30'"
    />
    <div
      class="absolute bottom-20 right-10 w-96 h-96 rounded-full blur-3xl animate-float-slow"
      :class="isDark ? 'bg-blue-500/10' : 'bg-blue-300/30'"
    />

    <div class="relative z-10 max-w-7xl mx-auto px-6 flex flex-col lg:flex-row items-center gap-12">
      <!-- Avatar -->
      <div
        class="w-full lg:w-1/2 h-[400px] lg:h-[500px]"
        data-aos="fade-right"
        data-aos-duration="1000"
      >
        <Avatar3D />
      </div>

      <!-- Texto -->
      <div class="w-full lg:w-1/2 text-center lg:text-left">
        <p
          data-aos="fade-up"
          data-aos-delay="200"
          class="text-lg mb-2"
          :class="isDark ? 'text-purple-400' : 'text-purple-600'"
        >
          Olá, eu sou
        </p>
        <h1
          data-aos="fade-up"
          data-aos-delay="400"
          class="text-5xl lg:text-7xl font-bold mb-4"
          :class="isDark ? 'text-white' : 'text-gray-900'"
        >
          Iago Fernandes Bastos
        </h1>
        <div
          data-aos="fade-up"
          data-aos-delay="600"
          class="h-1 w-24 bg-gradient-to-r from-purple-500 to-blue-500 mb-6 mx-auto lg:mx-0"
        />
        <p
          data-aos="fade-up"
          data-aos-delay="700"
          class="text-xl lg:text-2xl mb-8"
          :class="isDark ? 'text-gray-300' : 'text-gray-700'"
        >
          <span class="text-purple-600 dark:text-purple-400">
            Transformando ideias em
          </span>
          <span class="text-purple-600 dark:text-purple-400 font-bold ml-2 inline-block min-w-[120px] text-left">
            {{ typedWord }}<span class="animate-pulse">|</span>
          </span>
        </p>

        <!-- Redes sociais -->
        <div
          data-aos="fade-up"
          data-aos-delay="800"
          class="flex gap-4 justify-center lg:justify-start mb-8"
        >
          <a
            v-for="(social, index) in socialLinks"
            :key="index"
            :href="social.url"
            target="_blank"
            rel="noopener noreferrer"
            class="p-3 rounded-full backdrop-blur-sm transition-all duration-300 hover:scale-110 hover:bg-opacity-20"
            :class="isDark ? 'bg-white/10 hover:bg-white/20' : 'bg-gray-900/10 hover:bg-gray-900/20'"
          >
            <component :is="social.icon" class="w-6 h-6" />
          </a>
        </div>

        <button
          @click="scrollToAbout"
          data-aos="fade-up"
          data-aos-delay="900"
          class="px-8 py-3 rounded-full bg-gradient-to-r from-purple-500 to-blue-500 text-white font-semibold hover:shadow-lg hover:shadow-purple-500/50 transition-all duration-300 hover:scale-105"
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

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { Github, Linkedin, Mail, ArrowDown } from 'lucide-vue-next'
import { WhatsAppIcon } from 'vue3-simple-icons' // WhatsApp oficial
import Avatar3D from './Avatar3D.vue'

defineProps({
  isDark: Boolean
})

// Lista de palavras para o efeito de digitação
const words = ['código', 'soluções', 'realidade']
const typedWord = ref('')
let currentIndex = 0
let isDeleting = false
let timeout

const typeEffect = () => {
  const fullText = words[currentIndex]
  if (isDeleting) {
    typedWord.value = fullText.substring(0, typedWord.value.length - 1)
  } else {
    typedWord.value = fullText.substring(0, typedWord.value.length + 1)
  }

  if (!isDeleting && typedWord.value === fullText) {
    // Terminou de digitar, espera um pouco e começa a apagar
    timeout = setTimeout(() => {
      isDeleting = true
      typeEffect()
    }, 2000)
  } else if (isDeleting && typedWord.value === '') {
    // Apagou tudo, passa para a próxima palavra
    isDeleting = false
    currentIndex = (currentIndex + 1) % words.length
    timeout = setTimeout(typeEffect, 500)
  } else {
    // Continua digitando ou apagando
    const speed = isDeleting ? 50 : 100
    timeout = setTimeout(typeEffect, speed)
  }
}

onMounted(() => {
  typeEffect()
})

onUnmounted(() => {
  clearTimeout(timeout)
})

const socialLinks = [
  { icon: Github, url: 'https://github.com/IagoFer' },
  { icon: Linkedin, url: 'https://linkedin.com/in/iago-fernandes-bastos' },
  { icon: Mail, url: 'mailto:iagofernandesbastos@gmail.com' },
  { icon: WhatsAppIcon, url: 'https://wa.me/5585997900737' }
]

const scrollToAbout = () => {
  document.getElementById('about')?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<style scoped>
@keyframes float {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(30px, 20px); }
}
@keyframes float-slow {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(-40px, -20px); }
}
.animate-float {
  animation: float 8s ease-in-out infinite;
}
.animate-float-slow {
  animation: float-slow 10s ease-in-out infinite;
}
</style>