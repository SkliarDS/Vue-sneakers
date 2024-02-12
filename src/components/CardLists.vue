<script setup>
import Card from './Card.vue';

const onClickAdd = () => {
    alert('Добаввить в корзину')

}
function onClickFavorite() {
    alert('Добавить в избранное');  
}
defineProps({
    items: Array
})
</script>

<template>
    <div class="grid auto-fill gap-8">	
        <Card 
        v-for="item in items" 
        :key="item.id"
        :imageUrl="item.imageUrl"
        :title="item.title" 
        :price="item.price"
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