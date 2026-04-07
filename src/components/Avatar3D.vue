<template>
  <div class="w-full h-full flex items-center justify-center relative group">

    <!-- CÍRCULO FIXO / CONTAINER LIMPO -->
    <div
      class="w-64 h-64 md:w-80 md:h-80 rounded-full overflow-hidden
             shadow-[0_20px_40px_-15px_rgba(0,0,0,0.3)] transition-transform duration-500 ease-out xl:group-hover:scale-[1.05]">
      <!-- IMAGEM COM ZOOM -->
      <img src="/src/assets/iago.png" alt="Iago Fernandes" class="
          w-full h-full
          object-cover
          object-[50%_63%]
          scale-[1.15]
          transition-transform duration-700 ease-out group-hover:scale-[1.2]
        " @error="handleImageError" />
    </div>

  </div>
</template>

<script setup>
// Fallback caso a imagem não seja encontrada
const handleImageError = (e) => {
  e.target.src = "/src/assets/iago.png"
}
</script>