<template>
  <section id="projects" class="mt-24">
    <div class="glass rounded-3xl p-10">
      <h2 class="text-4xl font-bold mb-8">{{ t.projectsTitle }}</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div v-for="project in projects" :key="project.title" class="bg-white/5 border-l-4 rounded-xl overflow-hidden hover:shadow-lg transition-shadow" :class="projectClass(project.title)">
          <!-- Main Image with Gallery Navigation -->
          <div class="h-48 bg-gradient-to-br from-slate-700 to-slate-900 flex items-center justify-center overflow-hidden relative group">
            <img 
              v-if="project.image" 
              :src="project.image" 
              :alt="project.title" 
              class="w-full h-full object-cover transition-transform group-hover:scale-105" 
              @error="handleImageError" 
            />
            <div v-else class="text-center text-gray-500 w-full h-full flex items-center justify-center">
              <span class="text-sm">Project Image</span>
            </div>
            
            <!-- Gallery indicator -->
            <div v-if="project.gallery && project.gallery.length > 0" class="absolute bottom-2 right-2 bg-black/60 text-white text-xs px-2 py-1 rounded">
              {{ getGalleryIndex(project.title) + 1 }}/{{ project.gallery.length }}
            </div>
          </div>
          
          <div class="p-5">
            <strong class="text-lg block mb-2">{{ project.title }}</strong>
            <p class="text-sm text-gray-300 mb-4">{{ project.description }}</p>
            
            <!-- Image Gallery Thumbnails -->
            <div v-if="project.gallery && project.gallery.length > 1" class="flex gap-2 overflow-x-auto">
              <button 
                v-for="(image, index) in project.gallery" 
                :key="index"
                @click="switchImage(project.title, index)"
                class="flex-shrink-0 w-12 h-12 rounded border-2 transition-all hover:scale-110 overflow-hidden"
                :class="getGalleryIndex(project.title) === index ? 'border-white' : 'border-gray-600 opacity-70 hover:opacity-100'"
              >
                <img :src="image" :alt="`${project.title} ${index + 1}`" class="w-full h-full object-cover" @error="handleImageError" />
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  t: Object,
  projects: Array
})

const galleryIndex = ref({})

const projectClass = title => {
  if (title.includes('Hospital')) return 'border-sky-400'
  if (title.includes('Rwanda')) return 'border-green-400'
  return 'border-purple-500'
}

const handleImageError = (event) => {
  // Fallback for missing images
  event.target.style.display = 'none'
}

const switchImage = (projectTitle, imageIndex) => {
  galleryIndex.value[projectTitle] = imageIndex
  // Update the main image by finding and updating the project
  const project = props.projects.find(p => p.title === projectTitle)
  if (project && project.gallery) {
    project.image = project.gallery[imageIndex]
  }
}

const getGalleryIndex = (projectTitle) => {
  return galleryIndex.value[projectTitle] || 0
}
</script>

