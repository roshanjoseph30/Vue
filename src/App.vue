<script setup>
import Header from './components/Header.vue'
import ProductList from './components/ProductList.vue'
import Carousel from './components/Carousel.vue'
import { ref } from 'vue'
const cartCount = ref(0)

const addToCart = () => {
    cartCount.value++
}
</script>

<template>
  <div class="header">
    <Header :cart-count="cartCount"/>
  </div>

  <div class="carousel">
    <Carousel/>
  </div>

  <div class="product-list">
    <ProductList @add-to-cart="addToCart"/>
  </div>
</template>
