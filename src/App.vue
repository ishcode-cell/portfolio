<template>
  <div :class="['overflow-x-hidden min-h-screen', themeClass]">
    <div class="bg-animation"></div>
    <div class="max-w-7xl mx-auto px-6 py-10">
      <div class="flex flex-col sm:flex-row items-center justify-between gap-4 mb-10">
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
      <TechSection :t="t" :techCards="techCards" />
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
import TechSection from './components/TechSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'
import { contact } from './data/portfolioData.js'

const currentLocale = ref('en')
const theme = ref('dark')

const translations = {
  en: {
    navHome: 'Home',
    navAbout: 'About',
    navSkills: 'Skills',
    navProjects: 'Projects',
    navContact: 'Contact',
    switchLight: 'Switch to Light Mode',
    switchDark: 'Switch to Dark Mode',
    heroIntro: "Hi, I'm",
    heroName: 'ISHEMA MUGISHA ALVA',
    heroDescription: 'I am a Software Developer who builds modern, fast and beautiful web applications. I transform ideas into digital products that attract users and solve real-world problems.',
    heroButton: 'Explore My Work',
    aboutTitle: 'About Me',
    aboutText: 'I specialize in building high-quality web applications using modern technologies. My focus is creating clean interfaces, smooth user experiences, and scalable architectures. Every project is designed to look premium, perform fast, and provide real value to users.',
    techTitle: 'Technologies',
    techCards: [
      {
        name: 'HTML',
        icon: 'logos:html-5',
        description: 'Semantic markup foundation for accessible web experiences.'
      },
      {
        name: 'CSS',
        icon: 'logos:css-3',
        description: 'Modern styling and animation for beautiful UI design.'
      },
      {
        name: 'JavaScript',
        icon: 'logos:javascript',
        description: 'Interactive, dynamic behavior for web interfaces.'
      },
      {
        name: 'Vue.js',
        icon: 'logos:vue',
        description: 'Reactive frontend framework for composable UI components.'
      },
      {
        name: 'React',
        icon: 'logos:react',
        description: 'Component-driven library for fast and scalable apps.'
      }
    ],
    projectsTitle: 'Projects',
    projects: [
      {
        title: 'Hospital Finder Platform',
        description: 'Global hospital discovery and appointment booking system.',
        image: '/projects/hospital-finder.svg'
      },
      {
        title: 'Rwanda Travel Website',
        description: 'Modern tourism platform with attractive user experience.',
        image: '/projects/rwanda-travel.svg'
      },
      {
        title: 'Developer Portfolio Builder',
        description: 'Automated portfolio generator for developers.',
        image: '/projects/portfolio-builder.svg'
      }
    ],
    contactTitle: 'Contact',
    emailLabel: 'Email',
    githubLabel: 'GitHub',
    phoneLabel: 'Phone number',
    contactDescription: 'Send a quick message if you have a project, question, or collaboration idea.',
    contactFormHeadline: 'Send a Message',
    contactNameLabel: 'Name',
    contactEmailLabel: 'Email address',
    contactMessageLabel: 'Message',
    contactMessagePlaceholder: 'Tell me about your project or question...',
    contactSubmit: 'Send Message',
    contactSuccessMessage: 'Thanks! Your message is sent successfully.',
    footerText: '© 2026 Ishema Mugisha Alva • Designed to Impress Recruiters'
  },
  rw: {
    navHome: 'Ahabanza',
    navAbout: 'Ibyanjye',
    navSkills: 'Ubumenyi',
    navProjects: 'Imishinga',
    navContact: 'Hamwe',
    switchLight: 'Hindura ku buryo bwera',
    switchDark: 'Hindura ku buryo bwijimye',
    heroIntro: 'Muraho, nitwa',
    heroName: 'ISHEMA MUGISHA ALVA',
    heroDescription: 'Ndi umutekinisiye wa software wubaka porogaramu za interineti zigezweho, zishya kandi nziza. Nshyira mu bikorwa ibitekerezo kugira ngo ntegurire abakoresha ibicuruzwa bifite agaciro.',
    heroButton: 'Reba Imirimo',
    aboutTitle: 'Ibyanjye',
    aboutText: 'Ndi umwuga wubaka porogaramu za interineti zifite ireme ukoresheje ikoranabuhanga rigezweho. Intego yanjye ni ugutanga interineti nziza, gukoresha neza no kwagura umusingi w’ikoranabuhanga. Buri mushinga ugamije kuba mwiza, wihuta kandi ugira akamaro ku bakoresha.',
    techTitle: 'Ikoranabuhanga',
    techCards: [
      {
        name: 'HTML',
        icon: 'logos:html-5',
        description: 'Imiterere y’urubuga ifatika kandi ibasha gusomwa.'
      },
      {
        name: 'CSS',
        icon: 'logos:css-3',
        description: 'Gushushanya kwa moderne no gutuma interface iboneka neza.'
      },
      {
        name: 'JavaScript',
        icon: 'logos:javascript',
        description: 'Imikorere yihuta kandi ituma urubuga rukora neza.'
      },
      {
        name: 'Vue.js',
        icon: 'logos:vue',
        description: 'Umurongo wubaka interineti wihuta kandi ufite isura nziza.'
      },
      {
        name: 'React',
        icon: 'logos:react',
        description: 'Isomero ryubaka porogaramu zikoze neza kandi zoroshye.'
      }
    ],
    projectsTitle: 'Imishinga',
    projects: [
      {
        title: 'Hospital Finder Platform',
        description: 'Sisitemu yo gushakisha ibitaro ku isi no gutegura gahunda y’ubuvuzi.',
        image: '/projects/hospital-finder.svg'
      },
      {
        title: 'Rwanda Travel Website',
        description: 'Urubuga rwa ba mukerarugendo ruzamura uburambe bw’abashyitsi.',
        image: '/projects/rwanda-travel.svg'
      },
      {
        title: 'Developer Portfolio Builder',
        description: 'Porogaramu igenzura ikora portfolios ku banyamwuga.',
        image: '/projects/portfolio-builder.svg'
      }
    ],
    contactTitle: 'Hamwe',
    emailLabel: 'Imeli',
    githubLabel: 'GitHub',
    phoneLabel: 'Telefoni',
    contactDescription: 'Ohereza ubutumwa cyangwa ubaze ikibazo niba ufite umushinga cyangwa igitekerezo.',
    contactFormHeadline: 'Ohereza Ubutumwa',
    contactNameLabel: 'Izina',
    contactEmailLabel: 'Aderesi ya Imeli',
    contactMessageLabel: 'Ubutumwa',
    contactMessagePlaceholder: 'Tangira unyibwire ku mushinga cyangwa ikibazo...',
    contactSubmit: 'Ohereza Ubutumwa',
    contactSuccessMessage: 'Murakoze! Ubutumwa bwawe bwakozwe neza.',
    footerText: '© 2026 Ishema Mugisha Alva • Yateguwe kugira ngo ishimishe'
  }
}

const t = computed(() => translations[currentLocale.value])
const techCards = computed(() => t.value.techCards)
const projectList = computed(() => t.value.projects)
const themeClass = computed(() => (theme.value === 'light' ? 'theme-light' : 'theme-dark'))
const themeButtonText = computed(() => (theme.value === 'dark' ? t.value.switchLight : t.value.switchDark))

const toggleTheme = () => {
  theme.value = theme.value === 'dark' ? 'light' : 'dark'
}

watchEffect(() => {
  const html = document.documentElement
  html.classList.toggle('theme-light', theme.value === 'light')
  html.classList.toggle('theme-dark', theme.value === 'dark')
})
</script>
