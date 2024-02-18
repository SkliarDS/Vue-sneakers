<script setup>
	import { onMounted, ref, watch, reactive, provide, computed } from 'vue';
	import axios from 'axios';
	import Header from './components/Header.vue';	
	import CardList from './components/CardLists.vue';
	import Draver from './components/Draver.vue'
	
	const items = ref([]);
	const cart = ref([]);
	const draverOpen = ref(false);

	const filters = reactive({
		sortBy: 'title',
		searchQuery: ''
	});
	const creatOrder = async () => {
		try {
			const {data} = await axios.post("https://d4357a15413dbff9.mokky.dev/cart", {
				items: cart.value,
				totalPrice: totalPrice.value
			})			
			cart.value =[]			
			return data
		} catch (err) {
			console.log('err:',err);
		}
	}
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
	const clickToCart =  (item) => {
		if(!item.isAdded){
			addToCart(item);
		} else {
			removeCart(item);
		}
	}
	/* Открытие aside */ 
	const openDriver = () => {
		draverOpen.value = true
	}
	/* Закрытие aside */
	const closeDriver = () => {
		draverOpen.value = false
	}
	/* Получение загчения из select */ 
	const onChangeSelect = (e) =>{
		filters.sortBy = e.target.value;
	}
	/* Получение загчения из search */
	const onInputSearch = (e) =>{
		filters.searchQuery = e.target.value;
	}
	/* Получение товаров из избраных */ 
	const fetchFavorite = async () => {
		try {
			const {data: favorites} = await axios.get(`https://d4357a15413dbff9.mokky.dev/favorites`)
			items.value = items.value.map(item => {
				const favorite = favorites.find(favorite => favorite.productId === item.id);
				if(!favorite){
					return item
				} 
				return {
					...item,
					isFavorite: true,
					favoriteId: favorite.id
				}
			});
		} catch (err) {
			console.log('err:',err);
		}
	};
	/* Добавления\удаление товаров из избраных */ 
	const addToFavorite = async (item) => {
		try {
			if(!item.isFavorite){
				const obj = {
					productId: item.id
				}
				item.isFavorite = true
				const {data} = await axios.post(`https://d4357a15413dbff9.mokky.dev/favorites`, obj)
				item.favoriteId = data.id
			} else {
				item.isFavorite = false
				await axios.delete(`https://d4357a15413dbff9.mokky.dev/favorites/${item.favoriteId}`)
				item.favoriteId = null
			}
		} catch(err) {
			console.log('err:',err);
		}
		
	}
	/* Получение товаров */ 
	const onFetchItems = async () => {
		try {
			const params = {
				sortBy: filters.sortBy
			}
			if(filters.searchQuery){
				params.title = `*${filters.searchQuery}*`
			}
			const {data} = await axios.get( `https://d4357a15413dbff9.mokky.dev/items?`, {params});			
			items.value = data.map(obj=>({
				...obj,
				isAdded: false,
				favoriteId: null,
				isFavorite: false
			}));
			
		} catch (err){
			console.log('error:',err);
		}
	}
	/* Хук при загрузки приложение запрос к API */ 
	onMounted( async () => {
		cart.value = JSON.parse(localStorage.getItem('carts')) || []

		await onFetchItems();
		await fetchFavorite();

		items.value = items.value.map((item) => ({
			...item,
			isAdded: cart.value.some((cartItem) => cartItem.id === item.id)
		}))
	});
	/* Просмотр изменений */ 
	watch(filters, onFetchItems);
	watch(cart, ()=>{
		items.value = items.value.map((item) => ({
			...item,
			isAdded: false,
		}))	
		
	})	
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
		vatPrice,
		creatOrder
	})

</script>

<template>	
	<Draver v-if="draverOpen" @close-driver="closeDriver"/>
	<div class="mx-auto w-4/5 bg-white rounded-3xl shadow-xl mt-14">		
		<Header :count-cart="countCart" :total-price="totalPrice"  @open-driver="openDriver"/>
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
			<CardList :items="items" @addToFavorite="addToFavorite" @click-to-cart="clickToCart"/>
		</div>
	</div>

</template>

<style scoped>


</style>
