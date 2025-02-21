<template>
  <nav class="fixed top-1/2 right-4 transform -translate-y-1/2 flex flex-col gap-3">
    <button
      v-for="(section, index) in sections"
      :key="index"
      class="w-4 h-4 hover:cursor-pointer rounded-full outline-2 outline-black transition-all"
      :style="{
        backgroundColor: section.bgColor,
        transform: activeIndex === index ? 'scale(1.5) ' : 'scale(1)',
      }"
      @click="scrollToSection(index)"
    />
  </nav>
</template>

<script>
import gsap from 'gsap'

export default {
  props: {
    activeIndex: Number,
    sections: Array,
    container: Object, // Recibe la referencia del contenedor principal
  },
  methods: {
    scrollToSection(index) {
      if (this.container) {
        gsap.to(this.container, {
          x: `-${index * 100}vh`,
          y: `-${index * 100}vh`,
          duration: 1,
          ease: 'power2.out',
        })
      }
      this.$emit('updateActiveIndex', index) // Emite el nuevo índice
    },
  },
}
</script>
