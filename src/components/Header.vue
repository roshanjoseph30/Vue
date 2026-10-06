<script setup>
import shoppingBag from '../assets/shopping-bag.png'
defineProps({
    cartCount: Number
})
</script>

<template>
  <div class="header">
      <div>
          <h1>Products</h1>
      </div>

      <div class="bag">
            <img :src="shoppingBag" alt="bag" />
            <span>{{ cartCount }}</span>
      </div>
  </div>
</template>

