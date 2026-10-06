<script setup>

const props = defineProps({
    product: Object
})

const emit = defineEmits(['add-to-cart'])

const addToCart = () => {

    emit('add-to-cart', props.product)

}

</script>

<template>

    <div class="product-card">

        <div class="product-image">

            <img
                :src="product.thumbnail"
                :alt="product.title"
            />

        </div>

        <h2>{{ product.title }}</h2>
        <div class="product-price">
            <p>${{ product.price }}</p>
            <button @click="addToCart">
                Add to Cart
            </button>
        </div>

    </div>

</template>

<style scoped>


.product-price {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
}

.product-price p {
    font-size: 20px;
    font-weight: bold;
}

.product-price button{
   height: 40px;
   width: 100px;
   font-weight: bold;
   background-color: #000;
   color: rgb(255, 255, 255);
   border: none;
   border-radius: 5px;
   padding: 5px 10px;
   cursor: pointer;
}
.product-price button:hover{
   background-color: #333;
}

</style>