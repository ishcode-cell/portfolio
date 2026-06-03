<template>
  <section id="skills" class="mt-24">
    <h2 class="text-4xl font-bold mb-10">{{ t.techTitle }}</h2>
    <div class="tech-grid">
      <div v-for="tech in techCards" :key="tech.name" class="tech-card glass rounded-3xl p-8 text-center">
        <Icon :icon="tech.icon" class="tech-icon" />
        <h3 class="mt-6 text-2xl font-semibold">{{ tech.name }}</h3>
        <p class="mt-3 text-slate-300 leading-7">{{ tech.description }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { Icon } from '@iconify/vue'

const props = defineProps({
  t: Object,
  techCards: Array
})
</script>
