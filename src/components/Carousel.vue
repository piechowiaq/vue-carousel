<script setup>

import { ref, onMounted } from "vue";

const currentSlide = ref(1);
const getSlideCount = ref(null)

onMounted(() => {
  getSlideCount.value = document.querySelectorAll(".slide").length;

} )

const nextSlide = () => {
  if(currentSlide.value === getSlideCount.value){
    currentSlide.value = 1;
    return;
  }
  currentSlide.value += 1;
}

const prevSlide = () => {
  if(currentSlide.value === 1){
    currentSlide.value = 1;
    return;
  }
  currentSlide.value -= 1;
}


</script>


<template>
  <div class="carousel">
    <slot :currentSlide="currentSlide" />
    <!-- Navigation -->
    <div class="navigate">
      <div class="toggle-page left">
        <i @click="prevSlide" class="fas fa-chevron-left"></i>
      </div>
      <div class="toggle-page right">
        <i @click="nextSlide" class="fas fa-chevron-right"></i>
      </div>
    </div>
  </div>

</template>


<style lang="scss" scoped>

.navigate {
  padding: 0 16px;
  height: 100%;
  width: 100%;
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;

  .toggle-page {
    display: flex;
    flex: 1;

  }

  .right {
    justify-content: flex-end;
  }

  i {
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    background-color: #6347c7;
    color: #ffffff;
  }
}

</style>