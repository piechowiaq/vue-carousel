<template>
  <div class="home">
    <Carousel class="carousel">
      <Slide v-for="(slide, index) in carouselSlides" :key="index">
        <div class="slide-info">
          <img :src="require(`../assets/${slide}.jpg`)" alt="">
        </div>
      </Slide>
    </Carousel>
  </div>
</template>

<script>

import Carousel from "@/components/Carousel.vue";
import Slide from "@/components/Slide.vue";


export default {
  name: 'Home',
  components: { Carousel, Slide },
  setup() {
    const carouselSlides = ["bg-1", "bg-2", "bg-3"];

    return {carouselSlides};

  },
}
</script>

<style scoped lang="scss">

.carousel {
  max-height: 100vh;
  height: 100vh;
}

</style>