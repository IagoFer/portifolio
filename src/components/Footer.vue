<template>
  <footer
    class="relative py-12"
    :class="
      isDark
        ? 'bg-gradient-to-t from-purple-950/20 to-black'
        : 'bg-gradient-to-t from-purple-50 to-white'
    "
  >
    <div class="max-w-7xl mx-auto px-6">
      <div class="flex flex-col items-center">
        <!-- Links sociais -->
        <div
          class="flex gap-6 mb-8"
        >
          <a
            v-for="(social, index) in socialLinks"
            :key="index"
            :href="social.url"
            target="_blank"
            rel="noopener noreferrer"
            class="p-3 rounded-full transition-colors"
            :class="isDark ? 'bg-white/5 hover:bg-white/10' : 'bg-gray-900/5 hover:bg-gray-900/10'"
          >
            <component :is="social.icon" class="w-6 h-6" />
          </a>
        </div>

        <!-- Copyright -->
        <div
          class="text-center"
        >
          <p class="flex items-center gap-2" :class="isDark ? 'text-gray-400' : 'text-gray-600'">
            © {{ currentYear }} Feito com
            <Heart class="w-4 h-4 text-red-500 animate-pulse" />
            por Iago Fernandes Bastos
          </p>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { Github, Linkedin, Mail, Heart } from 'lucide-vue-next'

defineProps({
  isDark: Boolean
})

const currentYear = new Date().getFullYear()

const socialLinks = [
  { icon: Github, url: 'https://github.com/iagofernandes' },
  { icon: Linkedin, url: 'https://linkedin.com/in/iago-fernandes-bastos' },
  { icon: Mail, url: 'mailto:iagofernandesbastos@gmail.com' }
]
</script>