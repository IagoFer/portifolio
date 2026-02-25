<template>
  <section
    class="relative py-24 overflow-hidden"
    :class="
      isDark
        ? 'bg-gradient-to-b from-black via-purple-950/10 to-black'
        : 'bg-gradient-to-b from-white via-purple-50 to-white'
    "
  >
    <div class="max-w-7xl mx-auto px-6">
      <!-- Título -->
      <div class="text-center mb-16" data-aos="fade-up">
        <h2
          class="text-4xl lg:text-6xl font-bold mb-4"
          :class="isDark ? 'text-white' : 'text-gray-900'"
        >
          Experiência
        </h2>
        <div class="h-1 w-24 bg-gradient-to-r from-purple-500 to-blue-500 mx-auto" />
      </div>

      <!-- Timeline -->
      <div class="relative">
        <!-- Linha central -->
        <div
          class="absolute left-8 lg:left-1/2 top-0 bottom-0 w-0.5"
          :class="isDark ? 'bg-purple-500/30' : 'bg-purple-300'"
        />

        <div
          v-for="(exp, index) in experiences"
          :key="exp.company"
          class="relative flex flex-col lg:flex-row mb-12 lg:mb-16"
          :class="index % 2 === 0 ? '' : 'lg:flex-row-reverse'"
        >
          <!-- Espaço reservado para alinhamento (metade da largura) -->
          <div class="lg:w-1/2"></div>

          <!-- Card e ponto da timeline -->
          <div
            class="relative lg:w-1/2 flex"
            :class="index % 2 === 0 ? 'lg:justify-start' : 'lg:justify-end'"
          >
            <!-- Ponto da timeline -->
            <div
              class="absolute left-6 lg:left-auto w-4 h-4 rounded-full bg-gradient-to-r from-purple-500 to-blue-500 z-10"
              :class="
                index % 2 === 0
                  ? 'lg:-left-1.5'
                  : 'lg:-right-2'
              "
              :data-aos="'zoom-in'"
              :data-aos-delay="index * 200 + 300"
            />

            <!-- Card -->
            <div
              class="ml-16 lg:ml-0 w-[calc(100%-4rem)] lg:w-[calc(100%-4rem)] p-6 rounded-xl backdrop-blur-sm transition-all cursor-pointer hover:scale-[1.02]"
              :class="[
                index % 2 === 0 ? 'lg:ml-6' : 'lg:mr-6',
                isDark
                  ? 'bg-white/5 border border-white/10 hover:bg-white/10'
                  : 'bg-white border border-gray-200 hover:shadow-xl'
              ]"
              :data-aos="index % 2 === 0 ? 'fade-right' : 'fade-left'"
              :data-aos-delay="index * 200"
            >
              <!-- Cabeçalho: ícone e empresa (sempre à esquerda) -->
              <div class="flex items-center gap-2 mb-2">
                <Briefcase class="w-5 h-5 flex-shrink-0" :class="isDark ? 'text-purple-400' : 'text-purple-600'" />
                <h3 class="text-2xl font-bold" :class="isDark ? 'text-white' : 'text-gray-900'">
                  {{ exp.company }}
                </h3>
              </div>

              <p class="text-lg font-semibold mb-2" :class="isDark ? 'text-purple-400' : 'text-purple-600'">
                {{ exp.role }}
              </p>

              <!-- Período (sempre à esquerda) -->
              <div class="flex items-center gap-2 mb-4">
                <Calendar class="w-4 h-4 flex-shrink-0" :class="isDark ? 'text-gray-400' : 'text-gray-600'" />
                <p class="text-sm" :class="isDark ? 'text-gray-400' : 'text-gray-600'">
                  {{ exp.period }}
                </p>
              </div>

              <p class="mb-4" :class="isDark ? 'text-gray-300' : 'text-gray-700'">
                {{ exp.description }}
              </p>

              <!-- Tags de tecnologia (sempre à esquerda) -->
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="tech in exp.technologies"
                  :key="tech"
                  class="px-3 py-1 rounded-full text-sm"
                  :class="
                    isDark
                      ? 'bg-purple-500/20 text-purple-300'
                      : 'bg-purple-100 text-purple-700'
                  "
                >
                  {{ tech }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { Briefcase, Calendar } from 'lucide-vue-next'

defineProps({
  isDark: Boolean
})

const experiences = [
  {
    company: 'Guardin System',
    role: 'Desenvolvedor Full Stack (Tech Lead front-end)',
    period: '10/2024 - 08/2025',
    description:
      'Atuação como Tech Lead no desenvolvimento de um sistema completo de rastreamento veicular, incluindo CRM, captação de leads, cotação, planos, comissões, chat, pipelines, dashboards e monitoramento de veículos. Atendimento a clientes em todo o Brasil (empresas privadas e públicas).',
    technologies: ['Java', 'PHP Laravel', 'Vue.js', 'Docker', 'PostgreSQL', 'Tailwind', 'Scrum']
  },
  {
    company: 'Fabrica Info',
    role: 'Desenvolvedor Full Stack Jr',
    period: '09/2022 - 01/2024',
    description:
      'Análise e desenvolvimento de sistemas para digitalização de documentos e processos. Desenvolvimento do sistema PROLEGIS para a Assembleia Legislativa do Ceará (ALECE) e do sistema NovoCFC para autoescolas de Fortaleza.',
    technologies: ['React.js', 'Node.js', 'PHP Laravel', 'Vue.js', 'Docker', 'PostgreSQL', 'Bitbucket', 'Scrum']
  },
  {
    company: 'DATAPREV',
    role: 'Desenvolvedor Web (Estágio)',
    period: '07/2021 - 09/2022',
    description:
      'Desenvolvimento de aplicações web com foco em backend Java e Spring Boot. Criação de novas funcionalidades, correção de bugs em sistemas legados e desenvolvimento de APIs REST.',
    technologies: ['Java', 'Spring Boot', 'JPA', 'SQL Server', 'PostgreSQL', 'React', 'Postman']
  },
  {
    company: 'SEPOG',
    role: 'Desenvolvedor Web (Estágio)',
    period: '09/2019 - 06/2021',
    description:
      'Desenvolvimento do sistema Bens e Imóveis, aplicação de layout e relatórios. Manutenção nos sistemas Aposentadoria e Patrimônio. Desenvolvimento full stack com Java, Spring Boot, JSF, PrimeFaces.',
    technologies: ['Java', 'Spring Boot', 'JSF', 'PrimeFaces', 'PostgreSQL', 'Git', 'Jira']
  }
]
</script>