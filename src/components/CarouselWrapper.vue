<template>
    <div class="carousel-wrapper">
        <slot :currentSlide="currentSlide" />

        <!-- navigation -->
        <div v-if="navigationEnabled" class="navigate">
            <div class="toggle-page left">
                <i @click="prevSlide" class="fa-solid fa-chevron-left"></i>
            </div>
            <div class="toggle-page right">
                <i @click="nextSlide" class="fa-solid fa-chevron-right"></i>
            </div>
        </div>

        <!-- pagination -->
        <div v-if="paginationEnabled" class="pagination">
            <span @click="goToSlide(index)" v-for="(slide, index) in getSlideCount" :key="index" :class="{ active : index + 1 === currentSlide }">
            </span>
        </div>
    </div>        
</template>

<script>
import { ref, onMounted } from "vue";

export default {
    props: ["startAutoPlay", "timeout", "navigation", "pagination"],
    setup(props) {
        const currentSlide = ref(1);
        const getSlideCount = ref(null);
        const autoPlayEnabled = ref(
            props.startAutoPlay === undefined ? true : props.startAutoPlay
        );
        const timeoutDuration = ref(
            props.timeout === undefined ? 5000 : props.timeout
        );
        const paginationEnabled = ref(
            props.pagination === undefined ? true : props.pagination
        );
        const navigationEnabled = ref(
            props.navigation === undefined ? true : props.navigation
        );

        // next slide
        const nextSlide = () => {
            if (currentSlide.value === getSlideCount.value) {
                currentSlide.value = 1;
                return;
            }
            currentSlide.value += 1; 
        }

        // prev slide
        const prevSlide = () => {
            if (currentSlide.value === 1) {
                currentSlide.value = 1;
                return;
            }
            currentSlide.value -= 1;
        }

        // pagination
        const goToSlide = (index) => {
            currentSlide.value = index + 1;
        }

        // autoplay
        const autoPlay = () => {
            setInterval(() => {
                nextSlide() 
            }, timeoutDuration.value)
        }

        if (autoPlayEnabled.value) {
            autoPlay();
        }

        onMounted(() => {
            getSlideCount.value = document.querySelectorAll(".carousel-slide").length;
            console.log(getSlideCount.value);
        }) 

        return { currentSlide, nextSlide, prevSlide, getSlideCount, goToSlide, paginationEnabled, navigationEnabled }
    }
};

</script>

<style lang="scss">
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

    .toggle-page :hover {
        opacity: 1 !important;
    }

    .right {
        justify-content: flex-end;
    }

    i {
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 50%;
        width: 40px;
        height: 40px;
        background-color: #6347c7;
        color: #fff;
        opacity: 0.6;
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
        width: 40px;
        height: 6px;
        /* border-radius: 50%; */
        background-color: #fff;
        box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
        opacity: 0.3;
    }
    
    .active {
        background-color: #6347c7;
        opacity: 0.8;
    }
}
</style>