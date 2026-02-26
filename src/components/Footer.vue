<template>
  <footer class="relative py-12 border-t" :class="isDark
      ? 'border-white/10 bg-gradient-to-t from-purple-950/20 to-black'
      : 'border-gray-200 bg-gradient-to-t from-purple-50 to-white'
    ">
    <div class="max-w-7xl mx-auto px-6">
      <div class="flex flex-col items-center">

        <!-- Social Links -->
        <div class="flex gap-6 mb-8">
          <a v-for="(social, index) in socialLinks" :key="index" :href="social.url" target="_blank"
            rel="noopener noreferrer" class="
              p-3
              rounded-full
              transition-all
              duration-300
              hover:scale-110
              hover:shadow-lg
              hover:shadow-indigo-500/20
            " :class="isDark
                ? 'bg-white/5 hover:bg-indigo-500/20'
                : 'bg-gray-900/5 hover:bg-indigo-500/10'
              ">
            <component :is="social.icon" class="w-6 h-6" />
          </a>
        </div>

        <!-- Copyright -->
        <div class="text-center">
          <p class="flex items-center gap-2" :class="isDark ? 'text-gray-400' : 'text-gray-600'">
            © {{ currentYear }} Iago Fernandes Bastos — Software Engineer
          </p>
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