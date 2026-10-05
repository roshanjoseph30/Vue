<script setup>
import { ref, onMounted } from 'vue'

const products = ref([])

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

onMounted(() => {
    fetchProducts()
})
</script>

<template>
    <div class="products">
        <div
            v-for="product in products"
            :key="product.id"
            class="product-card"
        >
            <img
                :src="product.thumbnail"
                :alt="product.title"
            />

            <h2>{{ product.title }}</h2>

            <p>${{ product.price }}</p>
        </div>
    </div>
</template>



