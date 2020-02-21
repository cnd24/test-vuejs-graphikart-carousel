<template>
    <div>
        <carousel>
            <carousel-slide v-for="n in slides" :key="n" :index="n - 1">
                <img src="https://picsum.photos/id/1015/600/400" alt="" width="100%">
            </carousel-slide>
        </carousel>
        <button @click.prevent="addSlide">Ajouter un slide</button>
    </div>
</template>

<script>
    import Carousel from './components/carousel/Carousel.vue'
    import CarouselSlide from "./components/carousel/CarouselSlide";

    export default {
        name: 'App',
        data() {
            return {
                slides: 5,
            }
        },
        components: {
            Carousel,
            CarouselSlide
        },
        methods: {
            addSlide() {
                this.slides ++
            }
        }
    }
</script>

<style>
    html, body {
      margin: 0;
    }
</style>