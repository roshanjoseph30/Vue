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

            <div class="description-box">
                {{ product.description }}
            </div>

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
   border-radius: 30px;
   padding: 5px 10px;
   cursor: pointer;
}
.product-price button:hover{
   background-color: #333;
}

.product-image {
    background-color: rgba(255, 255, 255, 0.403);
    border-radius: 30px
}
.product-image img {
    transition: transform 0.3s ease;
}

.product-image img:hover {
    transform: scale(1.05);
}


.product-card {
    position: relative;
}

.description-box {
    position: absolute;
    top: 0;
    left: 140px;
    z-index: 1;

    width: 250px;
    padding: 15px;

    background-color: white;
    border: 1px solid #ccc;
    border-radius: 30px;

    font-size: 14px;

    opacity: 0;
    visibility: hidden;
    transition: opacity 0.3s ease;
}

.product-image:hover .description-box {
    opacity: 0.8;
    visibility: visible;
}

</style>