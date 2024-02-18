<script setup>
import {inject} from 'vue';
import CartItem from './CartItem.vue';
const {cart, removeCart} = inject('cartActions')


</script>

<template>
    <div class="grid gap-y-2" v-auto-animate>	
        <CartItem v-for="item in cart" :key="item.id"
            :imageUrl="item.imageUrl"
            :title="item.title" 
            :price="item.price"
            @remove-cart="()=>removeCart(item)"
        />       
    </div>
</template>

<style scoped>
.auto-fill {    
    grid-template-columns: repeat(auto-fill, minmax(210px, 1fr));
}
</style>