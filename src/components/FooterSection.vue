<template>
  <footer class="text-center mt-24 text-slate-500">{{ t.footerText }}</footer>
</template>

<script setup>
const props = defineProps({
  t: Object
})
</script>
