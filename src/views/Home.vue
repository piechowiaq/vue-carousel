<template>
  <div class="home">
    <Carousel class="carousel">
      <Slide>
        <div>
          <p>Hello</p>
        </div>
      </Slide>
    </Carousel>


  </div>
</template>

<script>

import Carousel from "@/components/Carousel.vue";
import Slide from "@/components/Slide.vue";


export default {
  name: 'HomeView',
  components: { Carousel, Slide },
  setup() {

  }
}
</script>

<style scoped lang="scss">

.carousel {
  max-height: 100vh;
  height: 100vh;
}

</style>