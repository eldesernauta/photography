<template>
  <section
    class="w-screen h-screen flex items-center justify-center transition-colors duration-500"
    :style="{ backgroundColor: bgColor }"
  >
    <div class="w-[98%] h-[95%] bg-white flex flex-col justify-center items-center text-center">
      <h2 class="font-pamela text-8xl" :style="{ color: String(bgColor) }">
        {{ title }}
      </h2>
      <div class="mt-4">
        <img
          v-for="(image, index) in image"
          :key="index"
          :src="image"
          class="w-[300px] h-auto inline-block mx-2"
        />
      </div>

      <button
        class="relative hover:cursor-pointer flex items-center mt-8 w-[200px] h-[60px] overflow-hidden font-medium transition-all rounded-none group"
        :style="{ backgroundColor: bgColor }"
      >
        <span
          class="absolute top-0 right-0 inline-block w-4 h-4 transition-all duration-500 ease-in-out bg-indigo-700 rounded group-hover:-mr-4 group-hover:-mt-4"
          :style="{ backgroundColor: bgCorners }"
        >
          <span
            class="absolute top-0 right-0 w-5 h-5 rotate-45 translate-x-1/2 -translate-y-1/2 bg-white"
          ></span>
        </span>
        <span
          class="absolute bottom-0 rotate-180 left-0 inline-block w-4 h-4 transition-all duration-500 ease-in-out bg-indigo-700 rounded group-hover:-ml-4 group-hover:-mb-4"
          :style="{ backgroundColor: bgCorners }"
        >
          <span
            class="absolute top-0 right-0 w-5 h-5 rotate-45 translate-x-1/2 -translate-y-1/2 bg-white"
          ></span>
        </span>
        <span
          class="absolute bottom-0 left-0 w-full h-full transition-all duration-500 ease-in-out delay-200 -translate-x-full bg-black rounded-md group-hover:translate-x-0"
          :style="{ backgroundColor: bgCorners }"
        ></span>
        <span
          class="relative w-full text-center text-white transition-colors duration-200 ease-in-out group-hover:text-white"
          >{{ buttonText }}</span
        >
      </button>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    title: String,
    description: String,
    image: Array,
    buttonText: String,
    buttonUrl: String,
    bgColor: String,
    bgCorners: String,
  },
}
</script>
