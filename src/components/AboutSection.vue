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

      <!-- Marquee de tecnologias -->
      <div class="py-8 overflow-hidden" data-aos="fade-up" data-aos-delay="600">
        <div class="relative flex overflow-x-hidden">
          <div class="animate-marquee whitespace-nowrap flex gap-8">
            <div
              v-for="(tech, index) in [...techStack, ...techStack]"
              :key="index"
              class="inline-flex items-center gap-2 px-4 py-2 rounded-full"
              :class="isDark ? 'bg-white/5 border border-white/10' : 'bg-gray-100 border border-gray-200'"
            >
              <component :is="tech.icon" class="w-5 h-5" :class="isDark ? 'text-purple-400' : 'text-purple-600'" />
              <span class="text-sm font-medium" :class="isDark ? 'text-gray-300' : 'text-gray-700'">
                {{ tech.name }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import ImageWithFallback from './ImageWithFallback.vue'
import { Coffee } from 'lucide-vue-next' // Ícone para Java
import {
  SpringIcon,
  VueDotjsIcon,
  ReactIcon,
  NodeDotjsIcon,
  PhpIcon,
  LaravelIcon,
  DockerIcon,
  PostgreSqlIcon,
  GitIcon,
  TypeScriptIcon,
  JavaScriptIcon,
  Html5Icon,
  CssIcon,
  TailwindCssIcon,
  ScrumAllianceIcon
} from 'vue3-simple-icons'

defineProps({
  isDark: Boolean
})

const techStack = [
  { name: 'Java', icon: Coffee }, // Usa Coffee do Lucide
  { name: 'Spring', icon: SpringIcon },
  { name: 'Vue.js', icon: VueDotjsIcon },
  { name: 'React', icon: ReactIcon },
  { name: 'Node.js', icon: NodeDotjsIcon },
  { name: 'PHP', icon: PhpIcon },
  { name: 'Laravel', icon: LaravelIcon },
  { name: 'Docker', icon: DockerIcon },
  { name: 'PostgreSQL', icon: PostgreSqlIcon },
  { name: 'Git', icon: GitIcon },
  { name: 'TypeScript', icon: TypeScriptIcon },
  { name: 'JavaScript', icon: JavaScriptIcon },
  { name: 'HTML5', icon: Html5Icon },
  { name: 'CSS3', icon: CssIcon },
  { name: 'Tailwind', icon: TailwindCssIcon },
  { name: 'Scrum', icon: ScrumAllianceIcon },
]
</script>

<style scoped>
@keyframes marquee {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
.animate-marquee {
  animation: marquee 40s linear infinite;
}
</style>