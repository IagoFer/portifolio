<template>
    <section id="projects" class="relative py-24" :class="isDark ? 'bg-black' : 'bg-white'">

        <div class="max-w-7xl mx-auto px-6">

            <!-- TITLE -->
            <div class="text-center mb-16" data-aos="fade-up">
                <h2 class="text-4xl lg:text-6xl font-bold mb-4" :class="isDark ? 'text-white' : 'text-gray-900'">
                    Projetos
                </h2>

                <div class="h-1 w-24 bg-gradient-to-r from-purple-500 to-blue-500 mx-auto mb-4" />

                <p class="text-lg" :class="isDark ? 'text-gray-400' : 'text-gray-600'">
                    Confira alguns dos meus trabalhos e experiências profissionais
                </p>
            </div>

            <!-- GRID -->
            <div class="grid md:grid-cols-2 gap-8">

                <div v-for="(project, index) in projects" :key="project.name" :data-aos="'fade-up'"
                    :data-aos-delay="index * 100" class="group h-full hover:-translate-y-2 transition-transform">

                    <div class="h-full rounded-xl overflow-hidden cursor-pointer" :class="isDark
                        ? 'bg-white/5 border border-white/10 hover:bg-white/10'
                        : 'bg-white border border-gray-200 hover:shadow-2xl'">

                        <!-- IMAGE -->
                        <div class="relative h-48 overflow-hidden">
                            <ImageWithFallback :src="project.image" :alt="project.name"
                                class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500" />

                            <div class="absolute inset-0 bg-gradient-to-t from-black/80 to-transparent" />

                            <!-- LINKS -->
                            <div class="absolute inset-0 bg-purple-600/0 group-hover:bg-purple-600/20
transition-colors flex items-center justify-center gap-4
opacity-0 group-hover:opacity-100">

                                <a v-if="project.github" :href="project.github" target="_blank"
                                    class="p-3 bg-white/90 rounded-full hover:scale-110">
                                    <Github class="w-6 h-6 text-gray-900" />
                                </a>

                                <a v-if="project.demo" :href="project.demo" target="_blank"
                                    class="p-3 bg-white/90 rounded-full hover:scale-110">
                                    <ExternalLink class="w-6 h-6 text-gray-900" />
                                </a>

                            </div>
                        </div>

                        <!-- CONTENT -->
                        <div class="p-6">

                            <h3 class="text-2xl font-bold mb-3" :class="isDark ? 'text-white' : 'text-gray-900'">
                                {{ project.name }}
                            </h3>

                            <p class="mb-4" :class="isDark ? 'text-gray-300' : 'text-gray-700'">
                                {{ project.description }}
                            </p>

                            <!-- STACK -->
                            <div class="flex flex-wrap gap-2 mb-4">
                                <span v-for="tech in project.technologies" :key="tech"
                                    class="px-3 py-1 rounded-full text-sm" :class="isDark
                                        ? 'bg-purple-500/20 text-purple-300'
                                        : 'bg-purple-100 text-purple-700'">
                                    {{ tech }}
                                </span>
                            </div>

                            <!-- PROFESSIONAL META -->
                            <div class="pt-4 border-t space-y-4"
                                :class="isDark ? 'border-white/10' : 'border-gray-200'">

                                <!-- ROLE -->
                                <div class="grid grid-cols-2 gap-4">

                                    <div>
                                        <p class="text-xs uppercase tracking-wide text-gray-400">
                                            Tipo
                                        </p>
                                        <p class="text-sm font-semibold">
                                            {{ project.type }}
                                        </p>
                                    </div>

                                    <div>
                                        <p class="text-xs uppercase tracking-wide text-gray-400">
                                            Atuação
                                        </p>
                                        <p class="text-sm font-semibold">
                                            {{ project.role }}
                                        </p>
                                    </div>

                                </div>

                                <!-- IMPACT METRICS -->
                                <div class="flex flex-wrap gap-2">

                                    <span v-for="metric in project.metrics" :key="metric" class="px-3 py-1 text-xs rounded-full
bg-indigo-500/15 text-indigo-400
font-medium">
                                        {{ metric }}
                                    </span>

                                </div>
                            </div>

                        </div>
                    </div>
                </div>

            </div>

            <!-- GITHUB -->
            <div class="text-center mt-12">
                <a href="https://github.com/IagoFer" target="_blank" class="inline-flex items-center gap-2 px-8 py-3 rounded-full
bg-gradient-to-r from-purple-500 to-blue-500 text-white
font-semibold hover:scale-105">
                    <Github class="w-5 h-5" />
                    Ver mais no GitHub
                </a>
            </div>

        </div>
    </section>
</template>

<script setup>
import { Github, ExternalLink } from 'lucide-vue-next'
import ImageWithFallback from './ImageWithFallback.vue'

/* ===== ASSETS ===== */
import Workfy from '../assets/workfy_logo.png'
import Casamento from '../assets/Casamento.png'
import Luzeiros from '../assets/Luzeiros.png'
import Alece from '../assets/ALECE.png'
import NovoCFC from '../assets/NovoCFC.png'
import Oryon from '../assets/OryonSystem.png'
import Pokedex from '../assets/Pokemon.png'
import Sepog from '../assets/SEPOG.png'

defineProps({
    isDark: Boolean
})

const projects = [

    {
        name: "Workfy — Plataforma de Gestão RH",
        description:
            "Plataforma corporativa voltada à gestão organizacional, acompanhamento de colaboradores e análise de clima empresarial.",
        image: Workfy,
        technologies: ["Vue.js", "Laravel", "PostgreSQL", "Docker"],
        type: "Produto SaaS",
        role: "Arquitetura & Full Stack",
        metrics: [
            "Produto comercializado",
            "Módulos estratégicos RH",
            "Escalável multiempresa"
        ]
    },

    {
        name: "Sistema para Casamentos",
        description:
            "Solução digital para organização de eventos com gestão de presentes e automação de comunicação via WhatsApp.",
        image: Casamento,
        demo: "https://casamento-ochre.vercel.app/",
        technologies: ["Vue.js", "Laravel"],
        type: "Produto Comercial",
        role: "Full Stack Developer",
        metrics: [
            "Produto monetizado",
            "Automação de reservas",
            "Uso por múltiplos eventos"
        ]
    },

    {
        name: "Pokédex Interativa",
        description:
            "Aplicação analítica para comparação e exploração avançada de dados da API Pokémon.",
        image: Pokedex,
        demo: "https://pokedex-orpin-iota.vercel.app/",
        technologies: ["React", "REST API"],
        type: "Projeto Técnico",
        role: "Frontend Engineering",
        metrics: [
            "Consumo avançado API",
            "Data comparison",
            "Projeto analítico"
        ]
    },

    {
        name: "Landing Page Luzeiros Eventos",
        description:
            "Landing page institucional orientada à conversão e presença digital da marca.",
        image: Luzeiros,
        demo: "https://luzeiros-eventos.vercel.app/",
        technologies: ["Vue", "Tailwind"],
        type: "Projeto Cliente",
        role: "Frontend Developer",
        metrics: [
            "Projeto em produção",
            "Foco em conversão",
            "Cliente ativo"
        ]
    },

    {
        name: "Sistema de Rastreamento Veicular — Oryon",
        description:
            "Plataforma nacional de monitoramento e gestão de clientes e operações de rastreamento veicular.",
        image: Oryon,
        technologies: ["Vue.js", "Laravel", "Docker"],
        type: "Projeto Corporativo",
        role: "Tech Lead Frontend",
        metrics: [
            "Uso nacional",
            "Arquitetura padronizada",
            "Alta criticidade operacional"
        ]
    },

    {
        name: "PROLEGIS — ALECE",
        description:
            "Sistema legislativo responsável pelo fluxo digital de tramitações parlamentares.",
        image: Alece,
        technologies: ["React", "Node.js"],
        type: "Sistema Governamental",
        role: "Full Stack Developer",
        metrics: [
            "Sistema público",
            "Uso institucional",
            "Alta confiabilidade"
        ]
    },

    {
        name: "NovoCFC",
        description:
            "Plataforma completa para gestão administrativa e operacional de autoescolas.",
        image: NovoCFC,
        technologies: ["Vue.js", "Laravel"],
        type: "Projeto Corporativo",
        role: "Full Stack Developer",
        metrics: [
            "Clientes ativos",
            "Gestão operacional",
            "Sistema em produção"
        ]
    },

    {
        name: "Bens e Imóveis — SEPOG",
        description:
            "Sistema governamental de controle patrimonial e gestão de bens públicos.",
        image: Sepog,
        technologies: ["Java", "Spring Boot", "JSF"],
        type: "Sistema Governamental",
        role: "Full Stack Developer",
        metrics: [
            "Uso governamental",
            "Gestão patrimonial estadual",
            "Operação institucional"
        ]
    }

]
</script>