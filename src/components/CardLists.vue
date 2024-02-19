<script setup>
import Card from './Card.vue';

const emit = defineEmits(['addToFavorite', 'clickToCart']);

defineProps({
    items: Array,
    isFavorites: Boolean
})
</script>

<template>
    <div class="grid auto-fill gap-8" v-auto-animate>	
        <Card 
        v-for="item in items" 
        :key="item.id"
        :id="item.id"
        :imageUrl="item.imageUrl"
        :title="item.title" 
        :price="item.price"
        :isAdded="item.isAdded"
        :isFavorite="item.isFavorite"
        :onClickAdd=" ()=> emit('clickToCart', item)"
        :onClickFavorite="isFavorites ? null : ()=> emit('addToFavorite', item)"
        />
    </div>
</template>

<style scoped>
.auto-fill {    
    grid-template-columns: repeat(auto-fill, minmax(210px, 1fr));
}
</style>