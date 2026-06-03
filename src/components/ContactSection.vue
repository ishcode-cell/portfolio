<template>
  <section class="mt-24">
    <div class="glass rounded-3xl p-10">
      <h2 class="text-4xl font-bold mb-6">{{ t.contactTitle }}</h2>
      <div class="space-y-3 text-slate-300 text-lg">
        <p>{{ t.emailLabel }}: {{ contact.email }}</p>
        <p>{{ t.githubLabel }}: {{ contact.github }}</p>
        <p>{{ t.phoneLabel }}: {{ contact.phone }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
const props = defineProps({
  t: Object,
  contact: Object
})
</script>
