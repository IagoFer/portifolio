<template>
  <section id="about" class="relative py-24" :class="isDark ? 'bg-black' : 'bg-white'">
    <div class="max-w-7xl mx-auto px-6">
      <!-- Título -->
      <div class="text-center mb-16" data-aos="fade-up">
        <h2 class="text-4xl lg:text-6xl font-bold mb-4" :class="isDark ? 'text-white' : 'text-gray-900'">
          Quem está por trás do código
        </h2>
        <div class="h-1 w-24 bg-gradient-to-r from-purple-500 to-blue-500 mx-auto" />
      </div>

      <!-- Grid de conteúdo -->
      <div class="grid lg:grid-cols-2 gap-12 items-center mb-16">
        <div data-aos="fade-right" data-aos-delay="200" class="relative">
          <div class="relative overflow-hidden rounded-2xl shadow-2xl">
            <ImageWithFallback
              :src="Trabson"
              alt="Workspace" class="w-full h-[440px] lg:h-[480px] object-cover" />
            <div class="absolute inset-0" />
          </div>
        </div>

        <div data-aos="fade-left" data-aos-delay="400">
          <h3 class="text-3xl font-bold mb-6" :class="isDark ? 'text-white' : 'text-gray-900'">
            Desenvolvedor Full Stack & Tech Lead
          </h3>
          <p class="text-lg mb-4" :class="isDark ? 'text-gray-300' : 'text-gray-700'">
            Sou desenvolvedor Full Stack com mais de 7 anos de experiência criando produtos digitais escaláveis,
            performáticos e orientados a negócio. Recentemente atuei como Tech Lead Frontend na Oryon System, liderando
            o
            desenvolvimento de interfaces modernas e ajudando a equipe a construir software com qualidade e
            consistência.
          </p>

          <p class="text-lg mb-4" :class="isDark ? 'text-gray-300' : 'text-gray-700'">
            Minha trajetória começou no backend, desenvolvendo APIs com Java, 
            Laravel e Node.js. Essa base me permite enxergar o produto de ponta a ponta da arquitetura e
            regras de negócio até a experiência final do usuário.
          </p>

          <p class="text-lg" :class="isDark ? 'text-gray-300' : 'text-gray-700'">
            Gosto de transformar problemas reais em soluções bem estruturadas, colaborar com times e evoluir pessoas
            tecnicamente. Hoje meu foco está em construir sistemas escaláveis, fortalecer engenharia de software nos
            times e entregar produtos que realmente geram impacto.
          </p>
        </div>
      </div>

      <!-- Marquee de tecnologias -->
      <div class="py-8 overflow-hidden" data-aos="fade-up" data-aos-delay="600">
        <div class="relative flex overflow-x-hidden">
          <div class="animate-marquee whitespace-nowrap flex gap-8">
            <div v-for="(tech, index) in [...techStack, ...techStack]" :key="index"
              class="inline-flex items-center gap-2 px-4 py-2 rounded-full"
              :class="isDark ? 'bg-white/5 border border-white/10' : 'bg-gray-100 border border-gray-200'">
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
import { Coffee } from 'lucide-vue-next'
import Trabson from '../assets/Trabson.png'
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
  0% {
    transform: translateX(0);
  }

  100% {
    transform: translateX(-50%);
  }
}

.animate-marquee {
  animation: marquee 40s linear infinite;
}
</style>