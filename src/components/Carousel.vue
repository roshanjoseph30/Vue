<script setup>

import { ref, computed, onMounted, onUnmounted } from 'vue'

const products = ref([])
const currentIndex = ref(0)
const slideWidth = ref(0)
const isTransitioning = ref(true)
let interval
const API_URL = 'https://dummyjson.com/products?limit=100'

const fetchProducts = async () => {
    try {
        const response = await fetch(API_URL)
        if (!response.ok) {
            throw new Error('Failed to fetch products')
        }
        const data = await response.json()
        products.value = data.products

    } catch (error) {
        console.error(error)

    }

}
const updateSlideWidth = () => {
    const card = document.querySelector('.carousel-card')
    if (card) {
        slideWidth.value = card.offsetWidth + 25
    }

}
const carouselProducts = computed(() => {
    return [
        ...products.value,
        ...products.value
    ]

})

const nextSlide = () => {
    currentIndex.value++
}

const handleTransitionEnd = () => {
    if (currentIndex.value === products.value.length) {
        isTransitioning.value = false
        currentIndex.value = 0
        requestAnimationFrame(() => {
            requestAnimationFrame(() => {
                isTransitioning.value = true
            })
        })
    }
}


onMounted(async () => {
    await fetchProducts()
    updateSlideWidth()
    window.addEventListener('resize', updateSlideWidth)
    interval = setInterval(nextSlide, 2500)
})


onUnmounted(() => {
    clearInterval(interval)
    window.removeEventListener('resize', updateSlideWidth)

})
</script>

<template>

    <div class="carousel">

        <div class="carousel-track"
            :class="{ 'no-transition': !isTransitioning }"
            :style="{
                transform: `translateX(-${currentIndex * slideWidth}px)`
            }"
            @transitionend="handleTransitionEnd"
        >
            <div
                v-for="(product, index) in carouselProducts"
                :key="`${product.id}-${index}`"
                class="carousel-card"
            >
                <img
                    :src="product.thumbnail"
                    :alt="product.title"
                />
                <h2>{{ product.title }}</h2>
            </div>
        </div>
    </div>

</template>


<style scoped>

.carousel {
    width: 100%;
    overflow: hidden;
    margin: 40px 0;
}

.carousel-track {

    display: flex;
    gap: 30px;
    transition: transform 0.8s ease;

}

.carousel-track.no-transition {
    transition: none;

}


.carousel-card {
    flex: 0 0 calc((100% - 200px) / 5);
    background-color: rgba(255, 254, 254, 0.36);
    border-radius: 20px;
    border: 1px solid #ccc;
    padding: 20px;
    text-align: center;

}


.carousel-card img {
    width: 100%;
    height: 200px;
    object-fit: contain;

}

</style>