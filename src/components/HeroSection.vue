<template>
  <section id="home" class="flex flex-col lg:flex-row items-center justify-between gap-16">
    <div class="glass rounded-3xl p-10 transition-all duration-300 card-hover max-w-2xl">
      <h1 class="text-5xl md:text-7xl font-extrabold leading-tight">
        {{ t.heroIntro }}
        <span class="bg-gradient-to-r from-sky-400 via-purple-500 to-green-400 bg-clip-text text-transparent">{{ t.heroName }}</span>
      </h1>

      <p class="mt-6 text-slate-300 text-lg leading-8">{{ t.heroDescription }}</p>

      <a href="#projects" class="inline-block mt-8 px-8 py-4 rounded-xl font-bold text-black bg-gradient-to-r from-sky-400 to-purple-500 hover:scale-105 transition">
        {{ t.heroButton }}
      </a>
    </div>

    <img src="/photo.png" alt="Profile" class="profile w-80 h-[450px] object-cover rounded-3xl border-2 border-sky-400 shadow-2xl transition-all duration-500" />
  </section>
</template>

<script setup>
const props = defineProps({
  t: Object
})
</script>
