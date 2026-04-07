<template>
    <section id="projects" class="relative py-32 w-full bg-transparent">
        <div class="w-full max-w-[1400px] mx-auto px-6 md:px-12">

            <!-- TITLE (Asymmetric Left) -->
            <div class="mb-20 flex flex-col md:flex-row md:items-end justify-between gap-8" data-aos="fade-up">
                <div class="max-w-2xl">
                    <h2 class="text-4xl md:text-6xl font-bold tracking-tighter text-foreground mb-4">
                        Projetos
                    </h2>
                    <p class="text-lg md:text-xl text-muted-foreground leading-relaxed">
                        Confira alguns dos meus trabalhos e experiências profissionais
                    </p>
                </div>
            </div>

            <!-- MASONRY/GRID LIFTED -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-2 gap-8 md:gap-12">
                <div v-for="(project, index) in projects" :key="project.name" :data-aos="'fade-up'"
                    :data-aos-delay="(index % 2) * 100" class="group relative flex flex-col">

                    <!-- Clean Container, minimal 1px border, large radius -->
                    <div
                        class="flex flex-col h-full rounded-[2rem] border border-border bg-background transition-all duration-300 hover:bg-secondary/30 p-4 md:p-6">

                        <!-- IMAGE PREVIEW -->
                        <div
                            class="relative h-[250px] md:h-[320px] w-full rounded-[1.5rem] overflow-hidden mb-8 border border-border/50">
                            <ImageWithFallback :src="project.image" :alt="project.name"
                                class="w-full h-full object-cover transition-transform duration-700 ease-out group-hover:scale-105" />

                            <div
                                class="absolute inset-0 bg-background/0 group-hover:bg-background/20 transition-colors duration-500" />

                            <!-- ACTIONS -->
                            <div
                                class="absolute bottom-6 left-6 right-6 flex items-center justify-end gap-3 opacity-0 translate-y-4 group-hover:opacity-100 group-hover:translate-y-0 transition-all duration-500 delay-100">
                                <a v-if="project.github" :href="project.github" target="_blank"
                                    class="h-10 w-10 flex items-center justify-center bg-foreground text-background rounded-full hover:scale-105 transition-transform">
                                    <Github class="w-4 h-4" />
                                </a>
                                <a v-if="project.demo" :href="project.demo" target="_blank"
                                    class="h-10 w-10 flex items-center justify-center bg-foreground text-background rounded-full hover:scale-105 transition-transform">
                                    <ExternalLink class="w-4 h-4" />
                                </a>
                            </div>
                        </div>

                        <!-- CONTENT -->
                        <div class="flex-1 flex flex-col justify-between px-2">
                            <div>
                                <h3 class="text-2xl font-bold tracking-tight text-foreground mb-3">
                                    {{ project.name }}
                                </h3>
                                <p class="text-muted-foreground leading-relaxed mb-6">
                                    {{ project.description }}
                                </p>
                            </div>

                            <div class="space-y-6">
                                <!-- STACK -->
                                <div class="flex flex-wrap gap-2">
                                    <span v-for="tech in project.technologies" :key="tech"
                                        class="px-3 py-1 font-mono text-xs uppercase tracking-wider rounded-full border border-border bg-secondary text-foreground">
                                        {{ tech }}
                                    </span>
                                </div>

                                <!-- META DATA (Bento-style list) -->
                                <div class="grid grid-cols-2 gap-4 pt-4 border-t border-border">
                                    <div>
                                        <p
                                            class="text-[10px] font-mono tracking-widest uppercase text-muted-foreground mb-1">
                                            Tipo</p>
                                        <p class="text-sm font-medium text-foreground">{{ project.type }}</p>
                                    </div>
                                    <div>
                                        <p
                                            class="text-[10px] font-mono tracking-widest uppercase text-muted-foreground mb-1">
                                            Atuação</p>
                                        <p class="text-sm font-medium text-foreground">{{ project.role }}</p>
                                    </div>
                                </div>
                            </div>
                        </div>

                    </div>
                </div>
            </div>

            <!-- GITHUB CTA -->
            <div class="mt-20 flex justify-center w-full" data-aos="fade-up">
                <a href="https://github.com/IagoFer" target="_blank" class="
                    inline-flex items-center gap-3 px-8 py-4 rounded-full
                    border border-border bg-background text-foreground font-medium
                    transition-all hover:bg-foreground hover:text-background active:scale-[0.98]
                    shadow-[0_0_20px_rgba(0,0,0,0.02)]
                ">
                    <Github class="w-5 h-5" />
                    Explorar repositórios completos
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

const projects = [
    {
        name: "Workfy — Plataforma de Gestão RH",
        description: "Plataforma corporativa voltada à gestão organizacional, acompanhamento de colaboradores e análise de clima empresarial.",
        image: Workfy,
        technologies: ["Vue.js", "Laravel", "PostgreSQL", "Docker"],
        type: "Produto SaaS",
        role: "Arquitetura & Full Stack",
        metrics: ["Produto comercializado", "Módulos estratégicos RH"]
    },
    {
        name: "Sistema para Casamentos",
        description: "Solução digital para organização de eventos com gestão de presentes e automação de comunicação via WhatsApp.",
        image: Casamento,
        demo: "https://casamento-ochre.vercel.app/",
        technologies: ["Vue.js", "Laravel"],
        type: "Produto Comercial",
        role: "Full Stack Developer",
        metrics: ["Automação de reservas"]
    },
    {
        name: "Pokédex Interativa",
        description: "Aplicação analítica para comparação e exploração avançada de dados da API Pokémon.",
        image: Pokedex,
        demo: "https://pokedex-orpin-iota.vercel.app/",
        technologies: ["React", "REST API"],
        type: "Projeto Técnico",
        role: "Frontend Engineering",
        metrics: ["Consumo avançado API"]
    },
    {
        name: "Landing Page Luzeiros Eventos",
        description: "Landing page institucional orientada à conversão e presença digital da marca.",
        image: Luzeiros,
        demo: "https://luzeiros-eventos.vercel.app/",
        technologies: ["Vue", "Tailwind"],
        type: "Projeto Cliente",
        role: "Frontend Developer",
        metrics: ["Projeto em produção"]
    },
    {
        name: "Sistema de Rastreamento Veicular — Oryon",
        description: "Plataforma nacional de monitoramento e gestão de clientes e operações de rastreamento veicular.",
        image: Oryon,
        technologies: ["Vue.js", "Laravel", "Docker"],
        type: "Projeto Corporativo",
        role: "Tech Lead Frontend",
        metrics: ["Uso nacional", "Alta criticidade"]
    },
    {
        name: "PROLEGIS — ALECE",
        description: "Sistema legislativo responsável pelo fluxo digital de tramitações parlamentares.",
        image: Alece,
        technologies: ["React", "Node.js"],
        type: "Sistema Governamental",
        role: "Full Stack Developer",
        metrics: ["Uso institucional", "Confiabilidade"]
    },
    {
        name: "NovoCFC",
        description: "Plataforma completa para gestão administrativa e operacional de autoescolas.",
        image: NovoCFC,
        technologies: ["Vue.js", "Laravel"],
        type: "Projeto Corporativo",
        role: "Full Stack Developer",
        metrics: ["Clientes ativos", "Gestão operacional"]
    },
    {
        name: "Bens e Imóveis — SEPOG",
        description: "Sistema governamental de controle patrimonial e gestão de bens públicos.",
        image: Sepog,
        technologies: ["Java", "Spring Boot", "JSF"],
        type: "Sistema Governamental",
        role: "Full Stack Developer",
        metrics: ["Gestão patrimonial estadual"]
    }
]
</script>