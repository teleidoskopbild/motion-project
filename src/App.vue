<template>
  <div
    class="grid grid-cols-3 grid-rows-3 gap-2 sm:gap-4 h-screen bg-[url('/canvas.jpg')] bg-cover bg-center"
  >
    <div
      class="font-comico absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 font-bold text-black z-1 transition-all duration-500 ease-in-out"
      :class="{
        'hover:scale-110 hover:text-purple-700 hover:cursor-pointer ':
          counter >= 5,
      }"
      @mouseover="isHovered = true"
      @mouseleave="isHovered = false"
    >
      <h1
        class="text-center text-lg sm:text-base md:text-3xl lg:text-4xl xl:text-6xl"
      >
        MOTION PROJECT
      </h1>
      <h2
        class="text-center text-xs sm:text-base md:text-2xl lg:text-3xl xl:text-4xl"
      >
        ABSTRACT ART MUSEUM
      </h2>
      <img
        class="mx-auto mt-8 w-16 sm:w-24 animate-bounce"
        src="/scroll-down.svg"
        :class="{
          hidden: counter >= 3,
          block: counter < 3,
        }"
      />
    </div>

    <div
      class="flex flex-col justify-center bg-[url('/section5.jpg')] bg-cover bg-center row-span-2 transition-all duration-1500 ease-out"
      :class="{
        'opacity-100 translate-y-0': counter >= 5,
        'opacity-0 -translate-y-200': counter < 5,
        grayscale: isHovered && counter >= 5,
      }"
    >
      >
      <div
        v-show="isHovered && counter >= 5"
        class="text-white text-xl lg:text-3xl text-center"
      >
        <p class="font-comico text-center mb-6">Location</p>
        <p class="font-comico text-center">12 Art Avenue</p>
        <p class="font-comico text-center">Berlin, Germany</p>
        <p class="font-comico text-center mt-6">Entry Fee</p>
        <p class="font-comico text-center">€8</p>
      </div>
    </div>
    <div
      class="flex flex-col justify-center bg-[url('/section2.jpg')] bg-cover bg-center col-span-2 transition-all duration-1500 ease-in-out"
      :class="{
        'opacity-100 translate-y-0': counter >= 4,
        'opacity-0 -translate-y-200': counter < 4,
        grayscale: isHovered && counter >= 5,
      }"
    >
      <div
        v-show="isHovered && counter >= 5"
        class="text-white text-xl lg:text-3xl text-center"
      >
        <p class="font-comico text-center mb-6">OPENING HOURS</p>
        <p class="font-comico text-center">WED - FRI: 1:00 PM - 8:00 PM</p>
        <p class="font-comico text-center">SAT: 11:00 AM - 8:00 PM</p>
        <p class="font-comico text-center">SUN: CLOSED</p>
      </div>
    </div>
    <div
      class="bg-[url('/section3.jpg')] bg-cover bg-center col-span-1 row-span-1 transition-all duration-1500 ease-out"
      :class="{
        'opacity-100 translate-y-0': counter >= 3,
        'opacity-0 -translate-y-200': counter < 3,
      }"
    ></div>
    <div
      class="flex flex-col justify-center bg-[url('/section1.jpg')] bg-cover bg-center row-span-2 transition-all duration-1500 ease-out"
      :class="{
        'opacity-100 translate-y-0': counter >= 2,
        'opacity-0 -translate-y-200': counter < 2,
        grayscale: isHovered && counter >= 5,
      }"
    >
      <div
        v-show="isHovered && counter >= 5"
        class="text-white text-xl lg:text-3xl text-center"
      >
        <p class="font-comico text-center mb-6">VISIT US</p>
        <p class="font-comico text-center mb-6">EXPERIENCE ABSTRACT ART</p>
        <p class="font-comico text-center">SEE YOU SOON</p>
      </div>
    </div>
    <div
      class="flex flex-col justify-center bg-[url('/section4.jpg')] bg-cover bg-center col-span-2 transition-all duration-1500 ease-out"
      :class="{
        'opacity-100 translate-y-0': counter >= 1,
        'opacity-0 -translate-y-200': counter < 1,
        grayscale: isHovered && counter >= 5,
      }"
    >
      <div
        v-show="isHovered && counter >= 5"
        class="text-white text-xl lg:text-3xl text-center"
      >
        <p class="font-comico text-center mb-6">WORKS BY</p>
        <span class="font-comico text-center">LARS WIEGNER</span>
        <span class="font-comico text-center mr-2 ml-2">|</span>
        <span class="font-comico text-center">KOLLEKTIV 7</span>
        <span class="font-comico text-center mr-2 ml-2">|</span>
        <span class="font-comico text-center">MARA LIEBERT</span>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";

const counter = ref(0);
let scrollCount = 0;
const isHovered = ref(false);
const touchStartY = ref(0);

const handleScroll = (event) => {
  scrollCount++;

  if (scrollCount >= 5) {
    if (event.deltaY > 0) {
      counter.value = Math.min(counter.value + 1, 5);
    } else {
      counter.value = Math.max(counter.value - 1, 0);
    }
    scrollCount = 0;
  }
};

const handleTouchStart = (event) => {
  touchStartY.value = event.touches[0].clientY;
};

const handleTouchMove = (event) => {
  const touchEndY = event.touches[0].clientY;
  const deltaY = touchStartY.value - touchEndY;

  if (Math.abs(deltaY) > 30) {
    if (deltaY > 0) {
      counter.value = Math.min(counter.value + 1, 5);
    } else {
      counter.value = Math.max(counter.value - 1, 0);
    }
  }
};
onMounted(() => {
  window.addEventListener("wheel", handleScroll);
  window.addEventListener("touchstart", handleTouchStart);
  window.addEventListener("touchmove", handleTouchMove);
});
</script>
<style scoped></style>
