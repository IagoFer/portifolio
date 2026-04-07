<template>
    <section class="relative py-32 w-full bg-transparent">
        <div class="w-full max-w-[1400px] mx-auto px-6 md:px-12">

            <div class="mb-20 flex flex-col md:flex-row md:items-end justify-between gap-8" data-aos="fade-up">
                <div class="max-w-2xl">
                    <h2 class="text-4xl md:text-6xl font-bold tracking-tighter text-foreground mb-4">
                        Experiência
                    </h2>
                    <p class="text-lg md:text-xl text-muted-foreground leading-relaxed">
                        A trajetória técnica percorrida até o momento.
                    </p>
                </div>
            </div>

            <!-- Timeline Alternada -->
            <div class="relative w-full max-w-5xl mx-auto py-8">
                
                <!-- Linha Central (Desktop) / Linha Esquerda (Mobile) -->
                <div class="absolute left-6 md:left-1/2 transform md:-translate-x-1/2 top-0 bottom-0 w-px bg-border"></div>

                <div class="space-y-20">
                    <div v-for="(exp, index) in experiences" :key="exp.company" 
                         class="relative flex flex-col md:flex-row items-center w-full group"
                         :data-aos="'fade-up'" :data-aos-delay="index * 100">

                        <!-- Content Block -->
                        <!-- 
                            No Mobile: Sempre alinhado a direita da linha.
                            No Desktop: Alterna justify-end vs justify-start mudando sua Ordem no flex container.
                        -->
                        <div class="w-full md:w-1/2 pl-16 md:pl-0 flex transition-all duration-300 group-hover:-translate-y-1"
                             :class="index % 2 === 0 ? 'md:justify-end md:pr-12 md:text-right md:order-1' : 'md:justify-start md:pl-12 md:text-left md:order-2'">
                             
                            <div class="flex flex-col space-y-4 max-w-xl w-full"
                                 :class="index % 2 === 0 ? 'md:items-end' : 'md:items-start'">

                                <!-- Cabeçalho -->
                                <div class="flex items-center gap-3" :class="index % 2 === 0 ? 'md:flex-row-reverse' : ''">
                                    <div class="p-2 bg-secondary/50 rounded-lg border border-border shadow-sm">
                                        <Briefcase class="w-5 h-5 text-foreground" />
                                    </div>
                                    <h3 class="text-2xl font-bold tracking-tight text-foreground">{{ exp.company }}</h3>
                                </div>
                                
                                <!-- Pill Período -->
                                <div class="inline-flex items-center gap-2 px-3 py-1 bg-background rounded-full border border-border w-fit shadow-sm"
                                     :class="index % 2 === 0 ? 'md:flex-row-reverse' : ''">
                                    <Calendar class="w-4 h-4 text-muted-foreground" />
                                    <span class="text-sm font-medium text-foreground tracking-wide font-mono">{{ exp.period }}</span>
                                </div>

                                <!-- Texto -->
                                <p class="text-lg font-medium text-muted-foreground">{{ exp.role }}</p>
                                <p class="text-muted-foreground leading-relaxed py-2 md:max-w-md">{{ exp.description }}</p>
                                
                                <!-- Tecnologias -->
                                <div class="flex flex-wrap gap-2 pt-2"
                                     :class="index % 2 === 0 ? 'md:justify-end' : 'md:justify-start'">
                                    <span v-for="tech in exp.technologies" :key="tech" 
                                        class="px-2.5 py-1 rounded-md bg-secondary/30 text-foreground text-[11px] font-mono tracking-wider border border-border/50 uppercase">
                                        {{ tech }}
                                    </span>
                                </div>
                            </div>
                        </div>

                        <!-- Timeline Dot Mágico -->
                        <!-- Centralizado no eixo no Desktop, preso na esquerda no Mobile -->
                        <div class="absolute left-6 md:left-1/2 transform -translate-x-1/2 w-5 h-5 rounded-full bg-foreground border-[4px] border-background ring-2 ring-border/50 z-10 transition-all duration-300 group-hover:scale-125 group-hover:ring-foreground/50" />

                        <!-- Espaçador Desktop para criar a estrutura Zig-Zag -->
                        <div class="hidden md:block w-1/2" :class="index % 2 === 0 ? 'order-2' : 'order-1'"></div>
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
        role: 'Tech Lead Frontend • Full Stack Developer',
        period: '10/2024 — 11/2025',
        description:
            'Liderei o desenvolvimento frontend de uma plataforma nacional de rastreamento veicular, estruturando arquitetura de interfaces, padronização de componentes e fluxos críticos do produto. Atuei na evolução do CRM operacional, módulos comerciais e monitoramento em tempo real, suportando operações de clientes privados e públicos em todo o Brasil.',
        technologies: [
            'Vue.js',
            'Laravel',
            'Docker',
            'PostgreSQL',
            'Tailwind',
            'Scrum'
        ]
    },

    {
        company: 'Fábrica Info',
        role: 'Full Stack Developer',
        period: '09/2022 — 01/2024',
        description:
            'Atuei no desenvolvimento de sistemas corporativos e governamentais, participando da construção do PROLEGIS (ALECE) e do NovoCFC. Contribuí na modelagem de funcionalidades, integração entre serviços e evolução contínua de aplicações utilizadas em ambientes institucionais e operacionais.',
        technologies: [
            'React',
            'Node.js',
            'Vue.js',
            'Laravel',
            'Docker',
            'PostgreSQL',
            'Scrum'
        ]
    },

    {
        company: 'DATAPREV',
        role: 'Desenvolvedor Web',
        period: '07/2021 — 09/2022',
        description:
            'Desenvolvi e mantive aplicações backend utilizando Java e Spring Boot em sistemas de alta criticidade. Atuei na criação de APIs REST, manutenção de sistemas legados e melhoria da confiabilidade de serviços utilizados em operações previdenciárias nacionais.',
        technologies: [
            'Java',
            'Spring Boot',
            'JPA',
            'PostgreSQL',
            'SQL Server',
            'React'
        ]
    },

    {
        company: 'SEPOG — Governo do Estado do Ceará',
        role: 'Desenvolvedor Web',
        period: '09/2019 — 06/2021',
        description:
            'Participei do desenvolvimento do sistema Bens e Imóveis, responsável pela gestão patrimonial governamental. Atuei também na manutenção dos sistemas de Aposentadoria e Patrimônio, implementando funcionalidades, relatórios e melhorias estruturais em aplicações institucionais.',
        technologies: [
            'Java',
            'Spring Boot',
            'JSF',
            'PrimeFaces',
            'React.js',
            'HTML5',
            'Maven',
            'PostgreSQL',
            'Git',
            'Jira'
        ]
    }

]
</script>