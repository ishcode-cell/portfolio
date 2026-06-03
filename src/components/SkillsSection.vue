<template>
  <section class="mt-24">
    <h2 class="text-4xl font-bold mb-10">{{ t.skillsTitle }}</h2>
    <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
      <div v-for="skill in skills" :key="skill" class="glass p-6 rounded-2xl hover:border-purple-500 hover:scale-105 transition">
        {{ skill }}
      </div>
    </div>
  </section>
</template>

<script setup>
const props = defineProps({
  t: Object,
  skills: Array
})
</script>
