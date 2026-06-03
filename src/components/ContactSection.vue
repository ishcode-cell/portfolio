<template>
  <section id="contact" class="mt-24">
    <div class="glass rounded-3xl p-10 grid gap-10 lg:grid-cols-[minmax(280px,1fr)_1fr]">
      <div>
        <h2 class="text-4xl font-bold mb-6">{{ t.contactTitle }}</h2>
        <div class="space-y-3 text-slate-300 text-lg mb-8">
          <p>{{ t.emailLabel }}: {{ contact.email }}</p>
          <p>{{ t.githubLabel }}: {{ contact.github }}</p>
          <p>{{ t.phoneLabel }}: {{ contact.phone }}</p>
        </div>
        <p class="text-slate-300 leading-7">{{ t.contactDescription }}</p>
      </div>

      <div>
        <h3 class="text-3xl font-semibold mb-6">{{ t.contactFormHeadline }}</h3>
        <form @submit.prevent="handleSubmit" class="space-y-5">
          <label class="block text-slate-300">
            <span class="mb-2 block">{{ t.contactNameLabel }}</span>
            <input
              v-model="form.name"
              type="text"
              required
              class="w-full rounded-2xl border border-white/10 bg-white/5 px-4 py-3 text-white outline-none transition focus:border-sky-400"
              placeholder="Jane Doe"
            />
          </label>

          <label class="block text-slate-300">
            <span class="mb-2 block">{{ t.contactEmailLabel }}</span>
            <input
              v-model="form.email"
              type="email"
              required
              class="w-full rounded-2xl border border-white/10 bg-white/5 px-4 py-3 text-white outline-none transition focus:border-sky-400"
              placeholder="hello@example.com"
            />
          </label>

          <label class="block text-slate-300">
            <span class="mb-2 block">{{ t.contactMessageLabel }}</span>
            <textarea
              v-model="form.message"
              rows="5"
              required
              class="w-full rounded-2xl border border-white/10 bg-white/5 px-4 py-3 text-white outline-none transition focus:border-sky-400"
              :placeholder="t.contactMessagePlaceholder"
            ></textarea>
          </label>

          <button type="submit" class="rounded-2xl bg-gradient-to-r from-sky-400 to-purple-500 px-6 py-3 font-semibold text-slate-900 transition hover:scale-105">
            {{ t.contactSubmit }}
          </button>
        </form>

        <p v-if="success" class="mt-4 text-green-400">{{ t.contactSuccessMessage }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive, ref } from 'vue'

const props = defineProps({
  t: Object,
  contact: Object
})

const form = reactive({
  name: '',
  email: '',
  message: ''
})
const success = ref(false)

const handleSubmit = () => {
  success.value = true
  form.name = ''
  form.email = ''
  form.message = ''
  setTimeout(() => {
    success.value = false
  }, 5000)
}
</script>
