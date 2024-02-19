<script setup>
	import {  ref, watch, provide, computed } from 'vue';
	// import axios from 'axios';
	import Header from './components/Header.vue';		
	import Draver from './components/Draver.vue'
	
	
	const cart = ref([]);
	const draverOpen = ref(false);
	
	
	const totalPrice = computed(
		() => cart.value.reduce((acc, item) => acc + item.price, 0)
	);
	const countCart = computed(
		() => cart.value.length
	);
	const vatPrice = computed(
		() => Math.round(totalPrice.value * 0.05)
	)
	const addToCart =  (item) => {		
		item.isAdded = true
		cart.value.push(item)		
	}
	const removeCart =  (item) => {		
		cart.value.splice(cart.value.indexOf(item), 1)
		item.isAdded = false		
	}
	const openDriver = () => {
		draverOpen.value = true
	}
	const closeDriver = () => {
		draverOpen.value = false
	}
	
	watch(cart, ()=> {
		localStorage.setItem('carts', JSON.stringify(cart.value))
		
	}, {deep: true})

	/* Проброс пропсов от родителя к детям */ 
	provide('cartActions', {
		closeDriver,
		openDriver,
		cart,
		removeCart,
		addToCart,
		totalPrice,
		vatPrice
	})

</script>

<template>	
	<Draver v-if="draverOpen" @close-driver="closeDriver"/>
	<div class="mx-auto w-4/5 bg-white rounded-3xl shadow-xl my-14">		
		<Header :count-cart="countCart" :total-price="totalPrice"  @open-driver="openDriver"/>
		<div class="p-10">
			<router-view></router-view>
		</div>
	</div>
</template>

<style scoped>


</style>
