<script setup>
import Header from './components/Header.vue'
import ProductList from './components/ProductList.vue'
import Carousel from './components/Carousel.vue'

</script>

<template>
  <div class="header">
    <Header/>
  </div>

  <div class="carousel">
    <Carousel/>
  </div>

  <div class="product-list">
    <ProductList/>
  </div>
</template>
