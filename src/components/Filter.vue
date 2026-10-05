<script setup>
import { ref } from 'vue'

const searchText = ref('')
const selectedCategory = ref('')
</script>

<template>
    <div class="search">
        <input class="search-input"
            type="text"
            placeholder="Search products"
            v-model="searchText"
        />
    </div>

    <div class="category">
        <select class="category-select" v-model="selectedCategory">
            <option value="">All Categories</option>
        </select>

    </div>
</template>




