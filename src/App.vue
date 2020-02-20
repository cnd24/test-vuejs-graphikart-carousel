<template>
    <div>
        <carousel>
            <carousel-slide>
                <p>Salut les gens</p>
                <img src="https://picsum.photos/id/1015/600/400" alt="">
            </carousel-slide>
            <carousel-slide>
                <p>Aurevoir les gens</p>
                <img src="https://picsum.photos/id/1016/600/400" alt="">
            </carousel-slide>
        </carousel>
    </div>
</template>

<script>
    import Carousel from './components/carousel/Carousel.vue'
    import CarouselSlide from "./components/carousel/CarouselSlide";

    export default {
        name: 'App',
        components: {
            Carousel,
            CarouselSlide
        }
    }
</script>
