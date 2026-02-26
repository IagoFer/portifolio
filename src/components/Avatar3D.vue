<template>
  <div class="w-full h-full flex items-center justify-center">

    <!-- CÍRCULO FIXO -->
    <div
      class="w-64 h-64 rounded-full overflow-hidden
             border-4 border-purple-500 shadow-2xl"
    >
      <!-- IMAGEM COM ZOOM -->
      <img
        src="/src/assets/iago.png"
        alt="Iago Fernandes"
        class="
          w-full h-full
          object-cover
          object-[50%_63%]
          scale-125
          transition-transform duration-700
        "
        @error="handleImageError"
      />
    </div>

  </div>
</template>

<script setup>
// Fallback caso a imagem não seja encontrada
const handleImageError = (e) => {
    e.target.src = "/src/assets/iago.png"
}
</script>