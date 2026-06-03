<template>
  <div :class="['overflow-x-hidden min-h-screen', themeClass]">
    <div class="bg-animation"></div>
    <div class="max-w-7xl mx-auto px-6 py-10">
      <div class="flex flex-col sm:flex-row gap-4 items-center justify-between mb-10">
        <div class="flex items-center gap-3 flex-wrap text-sm uppercase tracking-[0.35em] text-slate-400">
          <span>{{ t.languageLabel }}</span>
          <select v-model="currentLocale" class="rounded-2xl px-4 py-2 bg-white/10 text-current border border-white/10 outline-none">
            <option value="en">English</option>
            <option value="rw">Kinyarwanda</option>
          </select>
        </div>

        <button @click="toggleTheme" :class="themeButtonClass" class="rounded-2xl px-4 py-2 font-semibold transition-all duration-200">
          {{ themeButtonText }}
        </button>
      </div>

      <HeroSection :t="t" />
      <AboutSection :t="t" />
      <SkillsSection :t="t" :skills="skillsList" />
      <ProjectsSection :t="t" :projects="projectList" />
      <ContactSection :t="t" :contact="contact" />
      <FooterSection :t="t" />
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watchEffect } from 'vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'
import { contact } from './data/portfolioData.js'

const currentLocale = ref('en')
const theme = ref('dark')

const translations = {
  en: {
    languageLabel: 'Language',
    switchLight: 'Switch to Light Mode',
    switchDark: 'Switch to Dark Mode',
    heroIntro: "Hi, I'm",
    heroName: 'ISHEMA MUGISHA ALVA',
    heroDescription: 'I am a Software Developer who builds modern, fast and beautiful web applications. I transform ideas into digital products that attract users and solve real-world problems.',
    heroButton: 'Explore My Work',
    aboutTitle: 'About Me',
    aboutText: 'I specialize in building high-quality web applications using modern technologies. My focus is creating clean interfaces, smooth user experiences, and scalable architectures. Every project is designed to look premium, perform fast, and provide real value to users.',
    skillsTitle: 'Skills',
    skills: [
      'HTML / CSS / JavaScript',
      'Vue.js / React',
      'UI / UX Design',
      'API Integration',
      'Problem Solving',
      'Git & GitHub'
    ],
    projectsTitle: 'Projects',
    projects: [
      {
        title: 'Hospital Finder Platform',
        description: 'Global hospital discovery and appointment booking system.'
      },
      {
        title: 'Rwanda Travel Website',
        description: 'Modern tourism platform with attractive user experience.'
      },
      {
        title: 'Developer Portfolio Builder',
        description: 'Automated portfolio generator for developers.'
      }
    ],
    contactTitle: 'Contact',
    emailLabel: 'Email',
    githubLabel: 'GitHub',
    phoneLabel: 'Phone number',
    footerText: '© 2026 Ishema Mugisha Alva • Designed to Impress Recruiters'
  },
  rw: {
    languageLabel: 'Ururimi',
    switchLight: 'Hindura ku buryo bwera',
    switchDark: 'Hindura ku buryo bwijimye',
    heroIntro: 'Muraho, nitwa',
    heroName: 'ISHEMA MUGISHA ALVA',
    heroDescription: 'Ndi umutekinisiye wa software wubaka porogaramu za interineti zigezweho, zishya kandi nziza. Nshyira mu bikorwa ibitekerezo kugira ngo ntegurire abakoresha ibicuruzwa bifite agaciro.',
    heroButton: 'Reba Imirimo',
    aboutTitle: 'Ibyanjye',
    aboutText: 'Ndi umwuga wubaka porogaramu za interineti zifite ireme ukoresheje ikoranabuhanga rigezweho. Intego yanjye ni ugutanga interineti nziza, gukoresha neza no kwagura umusingi w’ikoranabuhanga. Buri mushinga ugamije kuba mwiza, wihuta kandi ugira akamaro ku bakoresha.',
    skillsTitle: 'Ubumenyi',
    skills: [
      'HTML / CSS / JavaScript',
      'Vue.js / React',
      'Igishushanyo cya UI / UX',
      'Guhuza API',
      'Gukemura ibibazo',
      'Git & GitHub'
    ],
    projectsTitle: 'Imishinga',
    projects: [
      {
        title: 'Hospital Finder Platform',
        description: 'Sisitemu yo gushakisha ibitaro ku isi no gutegura gahunda y’ubuvuzi.'
      },
      {
        title: 'Rwanda Travel Website',
        description: 'Urubuga rwa ba mukerarugendo ruzamura uburambe bw’abashyitsi.'
      },
      {
        title: 'Developer Portfolio Builder',
        description: 'Porogaramu igenzura ikora portfolios ku banyamwuga.'
      }
    ],
    contactTitle: 'Hamwe',
    emailLabel: 'Imeli',
    githubLabel: 'GitHub',
    phoneLabel: 'Telefoni',
    footerText: '© 2026 Ishema Mugisha Alva • Yateguwe kugira ngo ishimishe'
  }
}

const t = computed(() => translations[currentLocale.value])
const skillsList = computed(() => t.value.skills)
const projectList = computed(() => t.value.projects)
const themeClass = computed(() => (theme.value === 'light' ? 'theme-light' : 'theme-dark'))
const themeButtonText = computed(() => (theme.value === 'dark' ? t.value.switchLight : t.value.switchDark))
const themeButtonClass = computed(() =>
  theme.value === 'dark'
    ? 'bg-white text-slate-900 hover:bg-white/90'
    : 'bg-slate-900 text-white hover:bg-slate-800'
)

const toggleTheme = () => {
  theme.value = theme.value === 'dark' ? 'light' : 'dark'
}

watchEffect(() => {
  const html = document.documentElement
  html.classList.toggle('theme-light', theme.value === 'light')
  html.classList.toggle('theme-dark', theme.value === 'dark')
})
</script>
