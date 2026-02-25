<template>
  <button
    @click="toggleTheme"
    class="fixed top-8 right-8 z-50 p-3 rounded-full backdrop-blur-lg border transition-colors"
    :class="isDark ? 'bg-white/10 border-white/20 hover:bg-white/20' : 'bg-black/10 border-black/20 hover:bg-black/20'"
    v-motion
    :while-hover="{ scale: 1.1 }"
    :while-tap="{ scale: 0.9 }"
  >
    <div :class="{ 'rotate-180': isDark }" class="transition-transform duration-500">
      <Sun v-if="isDark" class="w-6 h-6 text-yellow-400" />
      <Moon v-else class="w-6 h-6 text-purple-600" />
    </div>
  </button>
</template>

<script setup>
import { Sun, Moon } from 'lucide-vue-next'

defineProps({
  isDark: Boolean,
  toggleTheme: Function
})
</script>