<script setup>
import Header from './components/Header.vue'
import Filter from './components/Filter.vue'
import ProductList from './components/ProductList.vue'
</script>

<template>
  <div class="header">
    <Header/>
  </div>
  <div class="filter">
    <Filter/>
  </div>
  <div class="product-list">
    <ProductList/>
  </div>
</template>
