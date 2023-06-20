<template>
  <div class="home">
    <CarouselWrapper class="carousel-wrapper">
      <CarouselSlide>
        <div>
          <p>HELLO</p>
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
  }
}
</script>

<style lang="scss" scoped>
  .carousel-wrapper{
    max-height: 100vh;
    height: 100vh;
  }
</style>