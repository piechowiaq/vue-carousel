<script setup>

import { ref } from "vue";

const currentSlide = ref(1)


</script>


<template>
  <div class="carousel">
    <slot :currentSlide="currentSlide" />
  </div>

</template>


<style lang="scss" scoped>

</style>