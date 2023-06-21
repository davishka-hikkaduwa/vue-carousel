<template>
    <div class="carousel-wrapper">
        <slot :currentSlide="currentSlide" />

        <!-- navigation -->
        <div class="navigate">
            <div class="toggle-page left"></div>
        </div>
    </div>        
</template>

<script>
import { ref } from "vue";

export default {
    setup() {
        const currentSlide = ref(1);

        return { currentSlide }
    }
};

</script>

<style>

</style>