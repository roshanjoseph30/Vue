<script setup>
import ProductCard from './ProductCard.vue'
import { ref, onMounted, computed } from 'vue'

const products = ref([])

const searchText = ref('')
const selectedCategory = ref('')

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



const categories = computed(() => {
    return [...new Set(products.value.map(product => product.category))]
})


const filteredProducts = computed(() => {
    return products.value.filter(product => {

        const matchesSearch = product.title
            .toLowerCase()
            .includes(searchText.value.toLowerCase())

        const matchesCategory =
            selectedCategory.value === '' ||
            product.category === selectedCategory.value

        return matchesSearch && matchesCategory
    })
})

const emit = defineEmits(['add-to-cart'])

const addToCart = (product) => {
    console.log('Added to cart:', product)

    emit('add-to-cart', product)
}

onMounted(() => {
    fetchProducts()
})
</script>


<template>

    <div class="filter">
        <input
            v-model="searchText"
            type="text"
            placeholder="Search products..."
            class="search-input"
        />

        <select
            v-model="selectedCategory"
            class="category-select"
        >
            <option value="">
                All Categories
            </option>

            <option
                v-for="category in categories"
                :key="category"
                :value="category"
            >
                {{ category }}
            </option>
        </select>

    </div>


    <div class="products">

        <ProductCard
            v-for="product in filteredProducts"
            :key="product.id"
            :product="product"
            @add-to-cart="addToCart"
        />
        
    </div>

</template>
