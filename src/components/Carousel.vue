<script setup>

import { ref, onMounted, defineProps } from "vue";

const currentSlide = ref(1);
const getSlideCount = ref(null);
const autoPlayEnabled = ref(true);
const timeoutDuration = ref(3000);
const paginationEnabled = ref(props.pagination === undefined ? true : props.pagination);
const navigationEnabled = ref(props.navigation === undefined ? true : props.navigation);

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

const goToSlide = (index) => {
  currentSlide.value = index + 1
}

const autoPlay = () => {
  setInterval(() => {
    nextSlide()
  }, timeoutDuration.value)
}

if (autoPlayEnabled.value) {
  autoPlay();
}

const props = defineProps(["startAutoPlay", "timeout", "navigation",  "pagination"  ]);


</script>


<template>
  <div class="carousel">
    <slot :currentSlide="currentSlide" />
    <!-- Navigation -->
    <div  v-if="navigationEnabled" class="navigate">
      <div class="toggle-page left">
        <i @click="prevSlide" class="fas fa-chevron-left"></i>
      </div>
      <div class="toggle-page right">
        <i @click="nextSlide" class="fas fa-chevron-right"></i>
      </div>
    </div>
    <!-- Pagination -->
    <div v-if="paginationEnabled" class="pagination">
      <span v-for="(slide, index) in getSlideCount" :key="index" :class="{active : index + 1  === currentSlide }" @click="goToSlide(index)"></span>
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
.pagination {
  position: absolute;
  bottom: 24px;
  width: 100%;
  display: flex;
  gap: 16px;
  justify-content: center;
  align-items: center;

  span {
    cursor: pointer;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: white;
    box-shadow: 0 1px 3px 0 rgba(0,0,0,.1), 0 1px 2px 0 rgba(0, 0, 0 , 0.06) ;
  }

  .active {
    background-color: #6347c7;
  }
}
</style>