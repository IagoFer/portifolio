<template>
  <footer class="relative py-12 border-t border-border bg-transparent">
    <div class="max-w-7xl mx-auto px-6">
      <div class="flex flex-col items-center">

        <!-- Social Links -->
        <div class="flex gap-4 mb-8">
          <a v-for="(social, index) in socialLinks" :key="index" :href="social.url" target="_blank"
            rel="noopener noreferrer" class="
              p-3
              rounded-full
              border border-border bg-secondary/50
              transition-all
              hover:bg-foreground hover:text-background
              active:scale-[0.98]
            ">
            <component :is="social.icon" class="w-5 h-5" />
          </a>
        </div>

        <!-- Copyright -->
        <div class="text-center flex flex-col items-center gap-1 text-sm font-mono tracking-widest text-muted-foreground uppercase">
          <p>© {{ currentYear }} Iago Fernandes Bastos</p>
          <p>Software Engineer</p>
        </div>

      </div>
    </div>
  </footer>
</template>

<script setup>
import { Github, Linkedin, Mail } from 'lucide-vue-next'
import { WhatsAppIcon } from 'vue3-simple-icons'

defineProps({
  isDark: Boolean
})

const currentYear = new Date().getFullYear()

const socialLinks = [
  { icon: Github, url: 'https://github.com/IagoFer' },
  { icon: Linkedin, url: 'https://linkedin.com/in/iago-fernandes-bastos' },
  { icon: Mail, url: 'mailto:iagofernandesbastos@gmail.com' },
  { icon: WhatsAppIcon, url: 'https://wa.me/5585997900737' }
]
</script>