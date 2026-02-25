<template>
    <section class="relative py-24" :class="isDark ? 'bg-black' : 'bg-white'">
        <div class="max-w-7xl mx-auto px-6">
            <!-- Título -->
            <div class="text-center mb-16" data-aos="fade-up">
                <h2 class="text-4xl lg:text-6xl font-bold mb-4" :class="isDark ? 'text-white' : 'text-gray-900'">
                    Projetos
                </h2>
                <div class="h-1 w-24 bg-gradient-to-r from-purple-500 to-blue-500 mx-auto mb-4" />
                <p class="text-lg" :class="isDark ? 'text-gray-400' : 'text-gray-600'">
                    Confira alguns dos meus trabalhos recentes
                </p>
            </div>

            <!-- Grid de projetos -->
            <div class="grid md:grid-cols-2 gap-8">
                <div v-for="(project, index) in projects" :key="project.name" :data-aos="'fade-up'"
                    :data-aos-delay="index * 100" class="group h-full hover:-translate-y-2 transition-transform">
                    <div class="h-full rounded-xl overflow-hidden cursor-pointer" :class="isDark
                            ? 'bg-white/5 border border-white/10 hover:bg-white/10'
                            : 'bg-white border border-gray-200 hover:shadow-2xl'
                        ">
                        <!-- Imagem -->
                        <div class="relative h-48 overflow-hidden">
                            <ImageWithFallback :src="project.image" :alt="project.name"
                                class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500" />
                            <div class="absolute inset-0 bg-gradient-to-t from-black/80 to-transparent" />

                            <!-- Overlay com links -->
                            <div
                                class="absolute inset-0 bg-purple-600/0 group-hover:bg-purple-600/20 transition-colors flex items-center justify-center gap-4 opacity-0 group-hover:opacity-100">
                                <a :href="project.github" target="_blank" rel="noopener noreferrer"
                                    class="p-3 bg-white/90 rounded-full hover:bg-white transition-colors hover:scale-110">
                                    <Github class="w-6 h-6 text-gray-900" />
                                </a>
                                <a :href="project.demo" target="_blank" rel="noopener noreferrer"
                                    class="p-3 bg-white/90 rounded-full hover:bg-white transition-colors hover:scale-110">
                                    <ExternalLink class="w-6 h-6 text-gray-900" />
                                </a>
                            </div>
                        </div>

                        <!-- Informações -->
                        <div class="p-6">
                            <h3 class="text-2xl font-bold mb-3" :class="isDark ? 'text-white' : 'text-gray-900'">
                                {{ project.name }}
                            </h3>

                            <p class="mb-4" :class="isDark ? 'text-gray-300' : 'text-gray-700'">
                                {{ project.description }}
                            </p>

                            <div class="flex flex-wrap gap-2 mb-4">
                                <span v-for="tech in project.technologies" :key="tech"
                                    class="px-3 py-1 rounded-full text-sm" :class="isDark
                                            ? 'bg-purple-500/20 text-purple-300'
                                            : 'bg-purple-100 text-purple-700'
                                        ">
                                    {{ tech }}
                                </span>
                            </div>

                            <!-- Estatísticas -->
                            <div class="flex items-center gap-4 pt-4 border-t"
                                :class="isDark ? 'border-white/10' : 'border-gray-200'">
                                <div class="flex items-center gap-1">
                                    <Star class="w-4 h-4" :class="isDark ? 'text-yellow-400' : 'text-yellow-600'" />
                                    <span class="text-sm" :class="isDark ? 'text-gray-400' : 'text-gray-600'">
                                        {{ project.stars }}
                                    </span>
                                </div>
                                <div class="flex items-center gap-1">
                                    <GitFork class="w-4 h-4" :class="isDark ? 'text-gray-400' : 'text-gray-600'" />
                                    <span class="text-sm" :class="isDark ? 'text-gray-400' : 'text-gray-600'">
                                        {{ project.forks }}
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Botão ver mais -->
            <div class="text-center mt-12" data-aos="fade-up" data-aos-delay="200">
                <a href="https://github.com/IagoFer" target="_blank" rel="noopener noreferrer"
                    class="inline-flex items-center gap-2 px-8 py-3 rounded-full bg-gradient-to-r from-purple-500 to-blue-500 text-white font-semibold hover:shadow-lg hover:shadow-purple-500/50 transition-shadow hover:scale-105">
                    <Github class="w-5 h-5" />
                    Ver mais no GitHub
                </a>
            </div>
        </div>
    </section>
</template>

<script setup>
import { Github, ExternalLink, Star, GitFork } from 'lucide-vue-next'
import ImageWithFallback from './ImageWithFallback.vue'

defineProps({
    isDark: Boolean
})

const projects = [
    {
        name: 'E-commerce Platform',
        description:
            'Plataforma completa de e-commerce com painel administrativo, sistema de pagamentos e gestão de estoque.',
        image:
            'https://images.unsplash.com/photo-1603351130949-476794ec3dff?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=M3w3Nzg4Nzd8MHwxfHNlYXJjaHwxfHxjb2RpbmclMjBwcm9ncmFtbWluZyUyMGxhcHRvcCUyMHNjcmVlbnxlbnwxfHx8fDE3NzE4NjI2NDd8MA&ixlib=rb-4.1.0&q=80&w=1080',
        technologies: ['React', 'Node.js', 'MongoDB', 'Stripe'],
        github: 'https://github.com/seu-usuario/ecommerce-platform',
        demo: 'https://demo-ecommerce.com',
        stars: 234,
        forks: 56
    },
    {
        name: 'Task Management App',
        description:
            'Aplicativo de gerenciamento de tarefas com colaboração em tempo real, notificações e integração com calendário.',
        image:
            'https://images.unsplash.com/photo-1755436612906-60fbd2bffd69?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=M3w3Nzg4Nzd8MHwxfHNlYXJjaHwxfHxjcmVhdGl2ZSUyMHdvcmtzcGFjZSUyMGRlc2lnbiUyMG1pbmltYWx8ZW58MXx8fHwxNzcxODYyNjQ3fDA&ixlib=rb-4.1.0&q=80&w=1080',
        technologies: ['Next.js', 'TypeScript', 'Prisma', 'PostgreSQL'],
        github: 'https://github.com/seu-usuario/task-manager',
        demo: 'https://demo-tasks.com',
        stars: 187,
        forks: 42
    },
    {
        name: 'Social Media Dashboard',
        description:
            'Dashboard para análise de métricas de redes sociais com gráficos interativos e relatórios personalizados.',
        image:
            'https://images.unsplash.com/photo-1764204295508-37d89e699266?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=M3w3Nzg4Nzd8MHwxfHNlYXJjaHwxfHxhYnN0cmFjdCUyMGdyYWRpZW50JTIwYmFja2dyb3VuZCUyMHRlY2hub2xvZ3l8ZW58MXx8fHwxNzcxODYyNjQ2fDA&ixlib=rb-4.1.0&q=80&w=1080',
        technologies: ['Vue.js', 'D3.js', 'Firebase', 'Tailwind'],
        github: 'https://github.com/seu-usuario/social-dashboard',
        demo: 'https://demo-social.com',
        stars: 156,
        forks: 38
    },
    {
        name: 'AI Content Generator',
        description:
            'Ferramenta de geração de conteúdo usando IA com suporte para múltiplos idiomas e formatos.',
        image:
            'https://images.unsplash.com/photo-1546514714-df0ccc50d7bf?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=M3w3Nzg4Nzd8MHwxfHNlYXJjaHwxfHxtb2Rlcm4lMjBvZmZpY2UlMjB3b3Jrc3BhY2UlMjBkZXZlbG9wZXJ8ZW58MXx8fHwxNzcxODYyNjQ3fDA&ixlib=rb-4.1.0&q=80&w=1080',
        technologies: ['React', 'OpenAI API', 'Express', 'Redis'],
        github: 'https://github.com/seu-usuario/ai-content',
        demo: 'https://demo-ai.com',
        stars: 312,
        forks: 78
    }
]
</script>