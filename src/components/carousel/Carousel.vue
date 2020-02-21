<template>
    <div>
        <div class="carousel">
            <slot></slot>
            <button class="carousel-nav carousel-prev" @click.prevent="prev"> Prec. </button>
            <button class="carousel-nav carousel-next" @click.prevent="next"> Suiv. </button>
            <div class="carousel-pagination">
                <button v-for="n in slidesCount" :key="n" @click.prevent="paginate(n-1)"
                        :class="{active: n-1 == index}">
                </button>
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
                direction: 'right',
            }
        },
        mounted() {
            this.slides = this.$children
        },
        computed: {
            slidesCount() {
                return this.slides.length
            }
        },
        methods: {
            next() {
                this.index++
                this.direction = 'right'
                if (this.index >= this.slidesCount) {
                    this.index = 0
                }
            },
            prev() {
                this.index--
                this.direction = 'left'
                if (this.index < 0) {
                    this.index = this.slidesCount - 1
                }
            },
            paginate(n) {
                this.direction = n > this.index ? 'right' : 'left'
                this.index = n
            }
        }
    }
</script>

<style src="./carousel.css">

</style>
