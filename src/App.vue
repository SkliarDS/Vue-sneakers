<script setup>
import Header from './components/Header.vue';
import CardList from './components/CardLists.vue';
</script>

<template>
	
	<div class="mx-auto w-4/5 bg-white rounded-3xl shadow-xl mt-14">
		<Header/>
		<div class="p-10">
			<h2 class="text-3xl mb-8 font-bold">Все Кроссовки</h2>
			<CardList/>
		</div>
	</div>

</template>

<style scoped>


</style>
