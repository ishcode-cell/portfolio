<template>
  <section id="projects" class="mt-24">
    <div class="glass rounded-3xl p-10">
      <h2 class="text-4xl font-bold mb-8">{{ t.projectsTitle }}</h2>
      <div class="space-y-5">
        <div v-for="project in projects" :key="project.title" class="bg-white/5 border-l-4 p-5 rounded-xl" :class="projectClass(project.title)">
          <strong>{{ project.title }}</strong> — {{ project.description }}
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const props = defineProps({
  t: Object,
  projects: Array
})

const projectClass = title => {
  if (title.includes('Hospital')) return 'border-sky-400'
  if (title.includes('Rwanda')) return 'border-green-400'
  return 'border-purple-500'
}
</script>
