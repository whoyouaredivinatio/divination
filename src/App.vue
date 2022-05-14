<template>
  <TheDivination />
</template>

<script>
import TheDivination from "./components/TheDivination.vue";

export default {
  name: "App",
  components: {
    TheDivination,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

img {
  image-rendering: -moz-crisp-edges;
  image-rendering: -o-crisp-edges;
  image-rendering: -webkit-optimize-contrast;
  image-rendering: optimize-contrast;
  image-rendering: crisp-edges;
  image-rendering: pixelated;
  -ms-interpolation-mode: nearest-neighbor;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>
