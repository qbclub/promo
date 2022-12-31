<script setup>
import { onMounted, onUnmounted, ref } from "vue";
import gsap from "gsap";
import { useWindowSize } from "@vueuse/core";

const { width, height } = useWindowSize();

onMounted(() => {
  gsap.fromTo(
    "#text",
    {autoAlpha: 0.5}, {autoAlpha: 1, duration: 3, repeat: -1, yoyo: true, scale:1.5}
 
  );
  // gsap.to("#text", {
  //   x: 50,
  //   // rotation: 360,
  //   // and special properties
  //   duration: 2,
  // });
});
//
</script>

<template>
  <v-app-bar flat>
    <v-app-bar-title>
      <p id="text" class="text-center">З января с 10.00 до бесконечности</p>
    </v-app-bar-title>
  </v-app-bar>
</template>

<style lang="scss" scoped>

</style>

