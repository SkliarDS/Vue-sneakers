<script setup>
    import axios from 'axios';
	import debounce from 'lodash.debounce'
    import {onMounted, inject, reactive, watch, ref} from 'vue'    
    import CardList from '../components/CardLists.vue';

    const {cart, addToCart, removeCart} = inject('cartActions')

    const items = ref([]);
    const filters = reactive({
		sortBy: 'title',
		searchQuery: ''
	});

    const clickToCart =  (item) => {
		if(!item.isAdded){
			addToCart(item);
		} else {
			removeCart(item);
		}
	}
    
    const onChangeSelect = (e) =>{
		filters.sortBy = e.target.value;
	}
	
	const onInputSearch = debounce(
		(e) =>{
		filters.searchQuery = e.target.value;
	}, 600)

    const addToFavorite = async (item) => {
		try {
			if(!item.isFavorite){
				const obj = {
					item_id: item.id
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
    
	const fetchFavorite = async () => {
		try {
			const {data: favorites} = await axios.get(`https://d4357a15413dbff9.mokky.dev/favorites`)
			items.value = items.value.map(item => {
				const favorite = favorites.find(favorite => favorite.item_id === item.id);
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
	
	onMounted( async () => {
		cart.value = JSON.parse(localStorage.getItem('carts')) || []

		await onFetchItems();
		await fetchFavorite();

		items.value = items.value.map((item) => ({
			...item,
			isAdded: cart.value.some((cartItem) => cartItem.id === item.id)
		}))
	});

    watch(filters, onFetchItems);

    watch(cart, ()=>{
		items.value = items.value.map((item) => ({
			...item,
			isAdded: false,
		}))	
		
	})	

</script>

<template>
    <div class="flex justify-between items-center mb-8">
        <h1 class="text-3xl  font-bold">Все Кроссовки</h1>
        <div class="flex items-center gap-x-3">
			<div class="select_holder relative">
				<select @change="onChangeSelect" class="p-3 px-5 pr-10 border rounded-lg text-slate-400 focus:outline-slate-200" name="" id="">
					<option value="title">По названию</option>
					<option value="price">Дешевле</option>
					<option value="-price">Дороже</option>
				</select>
			</div>
            <input @input="onInputSearch" class="p-3 px-5 border rounded-lg focus:outline-slate-200" type="text" placeholder="Поиск..." >
        </div>
    </div>
    <CardList :items="items" @addToFavorite="addToFavorite" @click-to-cart="clickToCart"/>
</template>
<style scoped>
	select {
		-webkit-appearance: none;
		-moz-appearance: none;
		appearance: none;
		cursor: pointer;
	}
	.select_holder::before {
		position: absolute;
		content: ''; 
		width: 0;
		height: 0;
		border: 0 solid transparent;
		border-left-width: 6px;
		border-right-width: 6px;
		border-top: 6px solid rgb(148, 163, 184, .4);
		top: 50%;
		transform: translateY(-50%);
		right: 15px;
	}
</style>