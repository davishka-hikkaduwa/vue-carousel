<template>
  <div class="home">
    <CarouselWrapper
     :pagination="true" 
     :navigation="true"
     :startAutoPlay="true" 
     :timeout="5000" 
     class="carousel-wrapper" 
     v-slot="{ currentSlide }"
     >
      <CarouselSlide v-for="(slide, index) in carouselSlides" :key="index">
        <div class="slide-info" v-show="currentSlide === index + 1">
          <img :src="require(`../assets/${slide}.jpg`)" alt="">
        </div>
      </CarouselSlide>
    </CarouselWrapper>
  </div>
</template>

<script>
// @ is an alias to /src
import CarouselWrapper from '@/components/CarouselWrapper.vue';
import CarouselSlide from '@/components/CarouselSlide.vue';

export default {
  name: 'HomeView',
  components: {
    CarouselWrapper, CarouselSlide
  },
  setup() {
    const carouselSlides = ["bg-1", "bg-2", "bg-3"];

    return { carouselSlides };
  },
}
</script>

<style lang="scss" scoped>
  .carousel-wrapper {
    position: relative;
    max-height: 100vh;
    height: 100vh;

    .slide-info {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      max-height: 100%;
      height: 100%;

      img {
        min-width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }
  }
</style>