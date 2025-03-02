<template>
  <div class="grid grid-cols-3 grid-rows-3 gap-0 sm:gap-0 h-screen">
    <div
      class="bg-blue-500 row-span-2 transition-all duration-1500 ease-out"
      :class="{
        'opacity-100 translate-y-0': counter >= 5,
        'opacity-0 -translate-y-200': counter < 5,
      }"
    >
      Section 1
    </div>
    <div
      class="bg-green-500 col-span-2 transition-all duration-1500 ease-out"
      :class="{
        'opacity-100 translate-y-0': counter >= 4,
        'opacity-0 -translate-y-200': counter < 4,
      }"
    >
      Section 2
    </div>
    <div
      class="bg-red-500 col-span-1 row-span-1 transition-all duration-1500 ease-out"
      :class="{
        'opacity-100 translate-y-0': counter >= 3,
        'opacity-0 -translate-y-200': counter < 3,
      }"
    >
      Section 3
    </div>
    <div
      class="bg-yellow-500 row-span-2 transition-all duration-1500 ease-out"
      :class="{
        'opacity-100 translate-y-0': counter >= 2,
        'opacity-0 -translate-y-200': counter < 2,
      }"
    >
      Section 4
    </div>
    <div
      class="bg-purple-500 col-span-2 transition-all duration-1500 ease-out"
      :class="{
        'opacity-100 translate-y-0': counter >= 1,
        'opacity-0 -translate-y-200': counter < 1,
      }"
    >
      Section 5
    </div>
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";

const counter = ref(0);
let scrollCount = 0;

const handleScroll = (event) => {
  scrollCount++;

  if (scrollCount >= 6) {
    if (event.deltaY > 0) {
      counter.value = Math.min(counter.value + 1, 5);
    } else {
      counter.value = Math.max(counter.value - 1, 0);
    }
    scrollCount = 0;
  }
};

onMounted(() => {
  window.addEventListener("wheel", handleScroll);
});
</script>
<style scoped></style>
