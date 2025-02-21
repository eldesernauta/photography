<template>
  <main ref="container" id="backgrounddd" class="relative w-screen h-screen overflow-hidden">
    <div
      v-for="(section, index) in sections"
      :key="index"
      class="section z-10 flex items-center justify-center transition-all"
      :style="{
        backgroundColor: section.bgColor,
        zIndex: activeIndex === index ? 10 : 0,
      }"
    >
      <SectionTemplate
        :title="section.title"
        :image="section.image"
        :buttonText="section.buttonText"
        :buttonUrl="section.buttonUrl"
        :bgColor="section.bgColor"
        :bgCorners="section.bgCorners"
      />
    </div>
    <NavMenu
      class="z-50"
      :activeIndex="activeIndex"
      :sections="sections"
      @updateActiveIndex="scrollToSection"
    />
  </main>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue'
import SectionTemplate from '../Section/SectionTemplate.vue'
import NavMenu from '../Nav/NavMenu.vue'
import gsap from 'gsap'

export default {
  components: { SectionTemplate, NavMenu },
  setup() {
    const sections = ref([
      {
        title: 'Feliz vida',
        image: ['/src/assets/section1.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#694b9e',
        bgCorners: '#45306d',
      },
      {
        title: 'Nube Número Nueve',
        image: ['/src/assets/section2.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#364c74',
        bgCorners: '#16243d',
      },
      {
        title: 'Anosmia',
        image: ['/src/assets/section3.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#506d5d',
        bgCorners: '#244733',
      },
      {
        title: 'Tienes un gato en los ojos',
        image: ['/src/assets/section4.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#e7c447',
        bgCorners: '#b7962a',
      },
      {
        title: 'Morada & Rojo',
        image: ['/src/assets/section5.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#d87c45',
        bgCorners: '#9b4e22',
      },
      {
        title: 'Antojitos I',
        image: ['/src/assets/section6.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#924c66',
        bgCorners: '#592236',
      },
      {
        title: 'Otros y nosotros',
        image: ['/src/assets/section7.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#d8bcdb',
        bgCorners: '#8b698e',
      },
    ])

    const activeIndex = ref(0)
    const sectionsEl = ref([])

    const scrollToSection = (index) => {
      if (index === activeIndex.value) return
      const currentSection = sectionsEl.value[activeIndex.value]
      const nextSection = sectionsEl.value[index]

      gsap.set(nextSection, { x: '20vw', y: '20vh', zIndex: 10 })
      gsap.to(nextSection, {
        x: '0vw',
        y: '0vh',
        duration: 0.5,
        ease: 'bounce.inOut',
        onComplete: () => {
          gsap.set(currentSection, { zIndex: 0 })
        },
      })

      activeIndex.value = index
    }

    const handleScroll = (event) => {
      const direction = event.deltaY > 0 ? 1 : -1
      const newIndex = Math.max(
        0,
        Math.min(sections.value.length - 1, activeIndex.value + direction),
      )
      scrollToSection(newIndex)
    }

    onMounted(() => {
      sectionsEl.value = document.querySelectorAll('.section')
      window.addEventListener('wheel', handleScroll)
    })

    onUnmounted(() => {
      window.removeEventListener('wheel', handleScroll)
    })

    return { sections, activeIndex, scrollToSection }
  },
}
</script>

<style>
.section {
  width: 100vw;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
}
</style>
