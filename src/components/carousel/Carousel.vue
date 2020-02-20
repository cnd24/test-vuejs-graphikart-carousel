<template>
    <div>
        <div class="carousel">
            <slot></slot>
            <div class="carousel-btn">
                <button class="carousel-nav carousel-prev" @click.prevent="prev"> Prec. </button>
                <button class="carousel-nav carousel-next" @click.prevent="next"> Suiv. </button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                index: 0,
                slides: [],
            }
        },
        mounted() {
            this.slides = this.$children
            this.slides.forEach((slide, i) => {
                slide.index = i
            })
        },
        computed: {
            slidesCount() {
                return this.slides.length
            }
        },
        methods: {
            next() {
                this.index++
                if (this.index >= this.slidesCount) {
                    this.index = 0
                }
            },
            prev() {

                this.index--
                if (this.index < 0) {
                    this.index = this.slidesCount - 1
                }
            }
        }
    }
</script>

<style src="./carousel.css">

</style>
