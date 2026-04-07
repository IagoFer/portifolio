<template>
  <section id="about" class="relative py-32 w-full bg-transparent">
    <div class="max-w-7xl mx-auto px-6 md:px-12">
      <!-- Título -->
      <div class="mb-20 flex flex-col md:flex-row md:items-end justify-between gap-8" data-aos="fade-up">
        <div class="max-w-2xl">
          <h2 class="text-4xl md:text-5xl font-bold tracking-tighter text-foreground mb-4">
            Quem está por trás do código
          </h2>
        </div>
      </div>

      <!-- Grid de conteúdo -->
      <div class="grid lg:grid-cols-2 gap-16 lg:gap-24 items-center mb-24">
        <div data-aos="fade-right" data-aos-delay="200" class="relative">
          <div class="relative overflow-hidden rounded-[2rem] border border-border bg-background p-2">
            <ImageWithFallback :src="Trabson" alt="Workspace"
              class="w-full h-[440px] lg:h-[500px] object-cover rounded-[1.5rem]" />
          </div>
        </div>

        <div data-aos="fade-left" data-aos-delay="400" class="flex flex-col flex-1">
          <h3 class="text-3xl font-bold tracking-tight text-foreground mb-8">
            Desenvolvedor Full Stack & Tech Lead
          </h3>
          <div class="space-y-6 text-lg text-muted-foreground leading-relaxed">
            <p>
              Sou desenvolvedor Full Stack com mais de 7 anos de experiência criando produtos digitais escaláveis,
              performáticos e orientados a negócio. Recentemente atuei como Tech Lead Frontend na Oryon System,
              liderando o desenvolvimento de interfaces modernas e ajudando a equipe a construir software com
              qualidade e consistência.
            </p>
            <p>
              Minha trajetória começou no backend, desenvolvendo APIs com Java,
              Laravel e Node.js. Essa base me permite enxergar o produto de ponta a ponta da arquitetura e
              regras de negócio até a experiência final do usuário.
            </p>
            <p>
              Gosto de transformar problemas reais em soluções bem estruturadas, colaborar com times e
              evoluir pessoas tecnicamente. Hoje meu foco está em construir sistemas escaláveis,
              fortalecer engenharia de software nos times e entregar produtos que realmente geram impacto.
            </p>
          </div>
        </div>
      </div>

      <!-- Marquee de tecnologias -->
      <div class="py-8 overflow-hidden rounded-3xl border border-border bg-secondary/20" data-aos="fade-up"
        data-aos-delay="600">
        <div class="relative flex overflow-x-hidden">
          <div class="animate-marquee whitespace-nowrap flex gap-6 px-4">
            <div v-for="(tech, index) in [...techStack, ...techStack]" :key="index"
              class="inline-flex items-center gap-3 px-5 py-2.5 rounded-full border border-border bg-background">
              <component :is="tech.icon" class="w-5 h-5 text-foreground" />
              <span class="text-sm font-semibold tracking-wide text-foreground">
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