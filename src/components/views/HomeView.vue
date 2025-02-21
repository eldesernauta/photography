<template>
  <main
    ref="container"
    id="backgrounddd"
    class="flex flex-col lg:flex-row h-[600vh] w-screen overflow-visible"
  >
    <div v-for="(section, index) in sections" :key="index" class="snap-start section">
      <SectionTemplate
        :title="section.title"
        :description="section.description"
        :images="section.images"
        :buttonText="section.buttonText"
        :buttonUrl="section.buttonUrl"
        :bgColor="section.bgColor"
      />
    </div>
  </main>
  <NavMenu
    :activeIndex="currentIndex"
    :sections="sections"
    :container="container"
    @updateActiveIndex="(index) => (currentIndex = index)"
  />
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
        title: 'Sección 1',
        description: 'Fotografía de Naturaleza',
        images: ['img1.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#694b9e',
      },
      {
        title: 'Sección 2',
        description: 'Retratos Profesionales',
        images: ['img2.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#364c74',
      },
      {
        title: 'Sección 3',
        description: 'Eventos Especiales',
        images: ['img3.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#506d5d',
      },
      {
        title: 'Sección 4',
        description: 'Fotografía de Productos',
        images: ['img4.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#e7c447',
      },
      {
        title: 'Sección 5',
        description: 'Paisajes Urbanos',
        images: ['img5.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#d87c45',
      },
      {
        title: 'Sección 6',
        description: 'Fotografía en Blanco y Negro',
        images: ['img6.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#924c66',
      },
      {
        title: 'Sección 7',
        description: 'Fotografía Conceptual',
        images: ['img7.jpg'],
        buttonText: 'Ver Más',
        buttonUrl: '#',
        bgColor: '#d8bcdb',
      },
    ])

    const container = ref(null)
    const currentIndex = ref(0)

    const setPagePos = () => {
      const sectionsEl = document.querySelectorAll('.section')
      sectionsEl.forEach((section, index) => {
        section.style.transform = `translate(${index * 100}vh, ${index * 100}vh)`
      })
    }

    const handleScroll = (event) => {
      const direction = event.deltaY > 0 ? 1 : -1
      currentIndex.value = Math.max(
        0,
        Math.min(sections.value.length - 1, currentIndex.value + direction),
      )

      gsap.to(container.value, {
        x: `-${currentIndex.value * 100}vh`,
        y: `-${currentIndex.value * 90}vh`,
        duration: 1,
        ease: 'power2.out',
      })
    }

    onMounted(() => {
      setPagePos()
      window.addEventListener('wheel', handleScroll)
    })

    onUnmounted(() => {
      window.removeEventListener('wheel', handleScroll)
    })

    return { sections, container, currentIndex }
  },
}
</script>

<style>
main {
  display: flex;
  flex-wrap: nowrap;
  height: 100vh;
  width: 700vw;
  scroll-snap-type: mandatory;
}

.section {
  width: 100vw;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
}
</style>
