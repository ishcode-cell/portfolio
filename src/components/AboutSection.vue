<template>
  <section id="about" class="mt-24">
    <div class="glass rounded-3xl p-10 card-hover transition-all duration-300">
      <h2 class="text-4xl font-bold mb-5">{{ t.aboutTitle }}</h2>
      <p class="text-slate-300 leading-8 text-lg">{{ t.aboutText }}</p>
    </div>
  </section>
</template>

<script setup>
const props = defineProps({
  t: Object
})
</script>
