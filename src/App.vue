<template>
    <div>
        <carousel>
            <carousel-slide>
                Salut les gens
            </carousel-slide>
            <carousel-slide>
                Aurevoir les gens
            </carousel-slide>
        </carousel>
        <todos></todos>
    </div>
</template>

<script>
    import Todos from './components/Todos.vue'
    import Carousel from './components/carousel/Carousel.vue'
    import CarouselSlide from "./components/carousel/CarouselSlide";

    export default {
        name: 'App',
        components: {
            Todos,
            Carousel,
            CarouselSlide
        }
    }
</script>

<style>


</style>

