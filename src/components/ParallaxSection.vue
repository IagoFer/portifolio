<template>
  <div ref="el" :style="{ transform: `translateY(${y}px)` }" class="relative">
    <slot />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import { useScroll } from '@vueuse/core'

const props = defineProps({
  speed: { type: Number, default: 0.5 }
})

const el = ref(null)
const y = ref(0)

// Passamos a ref 'el' para o useScroll, não el.value
const { y: scrollY } = useScroll({ element: el })

watch(scrollY, (value) => {
  y.value = value * props.speed
})
</script>