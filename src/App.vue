<script setup>
	import { onMounted, ref, watch, reactive } from 'vue';

	import Header from './components/Header.vue';
	import CardList from './components/CardLists.vue';
	// import Draver from './components/Draver.vue'
	
	const items = ref([]);

	const filters = reactive({
		sortBy: '',
		searchQuery: ''
	});

	const onChangeSelect = (e) =>{
		filters.sortBy = e.target.value;
	}
	const onInputSearch = (e) =>{
		filters.searchQuery = e.target.value;
		console.log('e.target.value:',e.target.value);
	}

	const onFetchItems = async () => {
		try {
			const params = {
				sortByQuery: filters.sortBy,
				searchQuery: filters.searchQuery
			}
			const res = await fetch( `https://d4357a15413dbff9.mokky.dev/items?sortBy=${params.sortByQuery}&title=*${params.searchQuery}* `);
			const data  = await res.json();
			items.value = data;
		} catch (err){
			console.log('error:',err);
		}
	}

	onMounted(onFetchItems);
	watch(filters, onFetchItems);

</script>

<template>	
	<!-- <Draver/> -->
	<div class="mx-auto w-4/5 bg-white rounded-3xl shadow-xl mt-14">
		<Header/>
		<div class="p-10">
			<div class="flex justify-between items-center mb-8">
				<h2 class="text-3xl  font-bold">Все Кроссовки</h2>
				<div class="flex items-center gap-x-3">
					<select @change="onChangeSelect" class="p-3 px-5 border rounded-lg focus:outline-slate-200" name="" id="">
						<option value="title">По названию</option>
						<option value="price">Дешевле</option>
						<option value="-price">Дороже</option>
					</select>
					<input @input="onInputSearch" class="p-3 px-5 border rounded-lg focus:outline-slate-200" type="text" placeholder="Поиск..." >
				</div>
			</div>
			<CardList :items="items"/>
		</div>
	</div>

</template>

<style scoped>


</style>
