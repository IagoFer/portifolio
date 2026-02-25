<template>
    <img :src="srcWithFallback" :alt="alt" v-bind="$attrs" @error="handleError" />
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
    src: { type: String, required: true },
    alt: { type: String, default: '' },
    fallbackSrc: { type: String, default: "/src/assets/iago.png" }
})

const srcWithFallback = ref(props.src)

const handleError = () => {
    srcWithFallback.value = props.fallbackSrc
}

watch(() => props.src, (newSrc) => {
    srcWithFallback.value = newSrc
})
</script>