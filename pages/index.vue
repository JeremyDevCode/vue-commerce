<script setup lang="ts">
const route = useRoute()
</script>

<template>
  <div class="font-sans w-full min-h-screen bg-[#0D0F12] flex items-center justify-center text-[#E3E6E8]">
    <div class="flex flex-col items-center justify-center gap-20">
      <h1 class="text-6xl font-bold">Nuxt Routing set up successfully!</h1>

      <a class="flex flex-col gap-5 items-center text-5xl text-[#E3E6E8] visited:text-[#E3E6E8] no-underline font-medium hover:opacity-80 transition-all"
        href="./hayai">
        <img src="/aircase.png" />
        Come here Hayai</a>
    </div>
  </div>
</template>
