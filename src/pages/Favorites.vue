<script setup>
    import axios from 'axios';
    import {onMounted, ref, inject, watch} from 'vue'    
    import CardList from '../components/CardLists.vue'

    const favorites = ref([]);
    const items = ref([]);
    const {cart, addToCart, removeCart } = inject('cartActions')

   
    const clickToCart =  (item) => {
		if(!item.isAdded){
			addToCart(item);
		} else {
			removeCart(item);
		}
	}
    const getFavorites = async () => {
        try {
            const {data} = await axios.get('https://d4357a15413dbff9.mokky.dev/favorites?_relations=items')
            favorites.value = data.map(obj =>obj.item)
           
        } catch (err) {
            console.log('err:',err);
        }
    }
    onMounted( async () => {
        cart.value = JSON.parse(localStorage.getItem('carts')) || []
        await getFavorites()
        items.value = items.value.map((item) => ({
			...item,
			isAdded: cart.value.some((cartItem) => cartItem.id === item.id)
		}))
    });
    watch(cart, ()=>{
		items.value = items.value.map((item) => ({
			...item,
			isAdded: false,
		}))	
		
	})
</script>

<template>
    <div class="flex justify-between items-center mb-8"><h1 class="text-3xl  font-bold">Мои закладки</h1></div>    
    <CardList :items="favorites" @click-to-cart="clickToCart" is-favorites/> <!-- @addToFavorite="addToFavorite" @click-to-cart="clickToCart"  надо реализовать-->
</template>