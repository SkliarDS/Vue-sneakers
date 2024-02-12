<script setup>
import CartItem from './CartItem.vue';

</script>

<template>
    <div class="grid gap-y-2">	
        <CartItem 
        imageUrl="/sneakers/sneakers-1.jpg"
        title="Мужские Кроссовки Nike Blazer Mid Suede" 
        :price="4500"
        :isAdded="false"
        :isFavorite="false"
        :onClickAdd="onClickAdd"
        :onClickFavorite="onClickFavorite"
        />       
    </div>
</template>

<style scoped>
.auto-fill {    
    grid-template-columns: repeat(auto-fill, minmax(210px, 1fr));
}
</style>