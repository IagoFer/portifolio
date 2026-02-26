<template>
  <section class="relative min-h-screen flex flex-col justify-center items-center pb-28 md:pb-20">

    <!-- Background -->
    <div class="absolute inset-0" :class="isDark
      ? 'bg-gradient-to-br from-purple-900/20 via-black to-blue-900/20'
      : 'bg-gradient-to-br from-purple-100 via-white to-blue-100'" />

    <!-- Blobs -->
    <div class="absolute top-20 left-10 w-72 h-72 rounded-full blur-3xl animate-float"
      :class="isDark ? 'bg-purple-500/10' : 'bg-purple-300/30'" />
    <div class="absolute bottom-20 right-10 w-96 h-96 rounded-full blur-3xl animate-float-slow"
      :class="isDark ? 'bg-blue-500/10' : 'bg-blue-300/30'" />

    <div class="relative z-10 max-w-7xl mx-auto px-6 flex flex-col lg:flex-row items-center gap-12">

      <!-- Avatar -->
      <div class="w-full lg:w-1/2 h-[400px] lg:h-[500px]" data-aos="fade-right">
        <Avatar3D />
      </div>

      <!-- TEXT -->
      <div class="w-full lg:w-1/2 text-center lg:text-left">

        <p data-aos="fade-up" class="text-lg mb-2" :class="isDark ? 'text-purple-400' : 'text-purple-600'">
          Olá, eu sou
        </p>

        <h1 data-aos="fade-up" data-aos-delay="200" class="text-5xl lg:text-7xl font-bold mb-4"
          :class="isDark ? 'text-white' : 'text-gray-900'">
          Iago Fernandes Bastos
        </h1>

        <p data-aos="fade-up" data-aos-delay="300" class="text-xl font-semibold mb-6"
          :class="isDark ? 'text-gray-400' : 'text-gray-600'">
          Full Stack Developer • Tech Lead
        </p>

        <div class="h-1 w-24 bg-gradient-to-r from-purple-500 to-blue-500 mb-8 mx-auto lg:mx-0" />

        <!-- ROTATING VALUE -->
        <div data-aos="fade-up" data-aos-delay="400">
          <Transition name="fade-slide" mode="out-in">
            <p :key="currentPhrase" class="text-2xl lg:text-3xl font-medium mb-10 text-purple-500">
              {{ currentPhrase }}
            </p>
          </Transition>
        </div>

        <!-- SOCIAL -->
        <div class="flex gap-4 justify-center lg:justify-start mb-10" data-aos="fade-up">
          <a v-for="(social, index) in socialLinks" :key="index" :href="social.url" target="_blank"
            class="p-3 rounded-full backdrop-blur-sm transition-all duration-300 hover:scale-110" :class="isDark
              ? 'bg-white/10 hover:bg-white/20'
              : 'bg-gray-900/10 hover:bg-gray-900/20'">
            <component :is="social.icon" class="w-6 h-6" />
          </a>
        </div>

        <!-- CTA -->
        <button @click="scrollToProjects" data-aos="fade-up" data-aos-delay="600" class="
    px-10 py-4
    rounded-full
    bg-gradient-to-r from-indigo-600 to-violet-600
    text-white
    font-semibold
    transition-all duration-300
    hover:scale-105
    hover:shadow-lg
    hover:shadow-violet-500/30
    active:scale-95
  ">
          Explorar projetos
        </button>

      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="
    hidden sm:block
    absolute
    bottom-10
    md:bottom-10
    left-1/2
    -translate-x-1/2
    animate-bounce
    opacity-70
  ">
      <ArrowDown class="w-6 h-6" :class="isDark ? 'text-white/50' : 'text-gray-900/50'" />
    </div>

  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { Github, Linkedin, Mail, ArrowDown } from 'lucide-vue-next'
import { WhatsAppIcon } from 'vue3-simple-icons'
import Avatar3D from './Avatar3D.vue'

defineProps({
  isDark: Boolean
})

/* ===== ROTATING VALUE PROPOSITION ===== */

const phrases = [
  'Construindo sistemas escaláveis',
  'Liderando times técnicos',
  'Criando produtos de impacto'
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
  document.getElementById('about')
    ?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<style scoped>
@keyframes float {

  0%,
  100% {
    transform: translate(0, 0)
  }

  50% {
    transform: translate(30px, 20px)
  }
}

@keyframes float-slow {

  0%,
  100% {
    transform: translate(0, 0)
  }

  50% {
    transform: translate(-40px, -20px)
  }
}

.animate-float {
  animation: float 8s ease-in-out infinite;
}

.animate-float-slow {
  animation: float-slow 10s ease-in-out infinite;
}

/* TEXT TRANSITION */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all .5s ease;
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