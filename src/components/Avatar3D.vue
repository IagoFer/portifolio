<template>
    <div class="w-full h-full flex items-center justify-center">
        <img src="/src/assets/iago.png" alt="Iago Fernandes"
            class="rounded-full w-64 h-64 object-cover shadow-2xl border-4 border-purple-500"
            @error="handleImageError" />
    </div>
</template>

<script setup>
// Fallback caso a imagem não seja encontrada
const handleImageError = (e) => {
    e.target.src = "/src/assets/iago.png"
}
</script>