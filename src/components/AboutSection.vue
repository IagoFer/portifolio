<template>
  <section
    id="about"
    class="relative py-24"
    :class="isDark ? 'bg-black' : 'bg-white'"
  >
    <div class="max-w-7xl mx-auto px-6">
      <!-- Título -->
      <div class="text-center mb-16" data-aos="fade-up">
        <h2
          class="text-4xl lg:text-6xl font-bold mb-4"
          :class="isDark ? 'text-white' : 'text-gray-900'"
        >
          Sobre Mim
        </h2>
        <div class="h-1 w-24 bg-gradient-to-r from-purple-500 to-blue-500 mx-auto" />
      </div>

      <!-- Grid de conteúdo -->
      <div class="grid lg:grid-cols-2 gap-12 items-center mb-16">
        <div data-aos="fade-right" data-aos-delay="200" class="relative">
          <div class="relative overflow-hidden rounded-2xl shadow-2xl">
            <ImageWithFallback
              src="https://images.unsplash.com/photo-1546514714-df0ccc50d7bf?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=M3w3Nzg4Nzd8MHwxfHNlYXJjaHwxfHxtb2Rlcm4lMjBvZmZpY2UlMjB3b3Jrc3BhY2UlMjBkZXZlbG9wZXJ8ZW58MXx8fHwxNzcxODYyNjQ3fDA&ixlib=rb-4.1.0&q=80&w=1080"
              alt="Workspace"
              class="w-full h-[400px] object-cover"
            />
            <div class="absolute inset-0 bg-gradient-to-t from-purple-900/60 to-transparent" />
          </div>
        </div>

        <div data-aos="fade-left" data-aos-delay="400">
          <h3
            class="text-3xl font-bold mb-6"
            :class="isDark ? 'text-white' : 'text-gray-900'"
          >
            Desenvolvedor Full Stack apaixonado por tecnologia
          </h3>
          <p
            class="text-lg mb-4"
            :class="isDark ? 'text-gray-300' : 'text-gray-700'"
          >
            Formado em Ciência da Computação pela Estácio, com experiência em desenvolvimento web, mobile e software. Atuei como Tech Lead no front-end de um sistema completo de rastreamento veicular na Guardin System, utilizando Vue.js, Java e PHP Laravel.
          </p>
          <p
            class="text-lg mb-4"
            :class="isDark ? 'text-gray-300' : 'text-gray-700'"
          >
            Tenho sólidos conhecimentos em Java (Spring, JPA, JSF), JavaScript (React, Vue, Node), bancos de dados SQL e Docker. Sempre buscando aprender e aplicar as melhores práticas de desenvolvimento.
          </p>
          <p
            class="text-lg"
            :class="isDark ? 'text-gray-300' : 'text-gray-700'"
          >
            Atualmente focado em criar soluções escaláveis e eficientes, com forte atuação em equipes ágeis (Scrum). Disponível para oportunidades remotas ou híbridas.
          </p>
        </div>
      </div>

      <!-- Skills grid -->
      <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
        <div
          v-for="(skill, index) in skills"
          :key="skill.title"
          :data-aos="'fade-up'"
          :data-aos-delay="index * 100"
          class="p-6 rounded-xl backdrop-blur-sm transition-all cursor-pointer hover:scale-105"
          :class="
            isDark
              ? 'bg-white/5 border border-white/10 hover:bg-white/10'
              : 'bg-gray-50 border border-gray-200 hover:bg-gray-100'
          "
        >
          <component
            :is="skill.icon"
            class="w-12 h-12 mb-4"
            :class="isDark ? 'text-purple-400' : 'text-purple-600'"
          />
          <h4
            class="text-xl font-semibold mb-2"
            :class="isDark ? 'text-white' : 'text-gray-900'"
          >
            {{ skill.title }}
          </h4>
          <p :class="isDark ? 'text-gray-400' : 'text-gray-600'">
            {{ skill.desc }}
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { Code2, Palette, Zap, Users } from 'lucide-vue-next'
import ImageWithFallback from './ImageWithFallback.vue'

defineProps({
  isDark: Boolean
})

const skills = [
  { icon: Code2, title: 'Back-end', desc: 'Java • Spring • Node.js • PHP' },
  { icon: Palette, title: 'Front-end', desc: 'Vue • React • HTML5 • CSS3' },
  { icon: Zap, title: 'DevOps', desc: 'Docker • Git • CI/CD' },
  { icon: Users, title: 'Metodologias', desc: 'Scrum • Kanban • Liderança' }
]
</script>