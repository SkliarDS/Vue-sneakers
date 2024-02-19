<script setup>
    import { inject, ref } from 'vue';
	import axios from 'axios';
    import DraverHeader  from './DriverHeader.vue';
    import CartItemList from './CartItemList.vue'
    import DraverFooter from './DraverFooter.vue'
    import InfoBlock from './InfoBlock.vue';

    const {totalPrice, vatPrice, cart} = inject('cartActions')

    const orderId = ref(null)
    const emit = defineEmits(['closeDriver'])

    // const isCreatingOrder = ref(false)
    const creatOrder = async () => {
		try {
			const {data} = await axios.post("https://d4357a15413dbff9.mokky.dev/cart", {
				items: cart.value,
				totalPrice: totalPrice.value
			})			
			cart.value =[]	
            orderId.value = data.id		
			return data
		} catch (err) {
			console.log('err:',err);
		}
	}
</script>

<template>
    <div @click="()=>emit('closeDriver')" class="fixed top-0 left-0 w-screen h-screen bg-black z-10 opacity-50" v-auto-animate></div>
    <aside class="fixed  top-0 right-0 max-w-[420px] size-full h-screen bg-white z-20" v-auto-animate>
        <div class="p-10 flex flex-col h-full">
            <DraverHeader/>
            <CartItemList  />
            <div  v-if="!totalPrice || itemId" class="flex items-center  justify-center w-full h-full" v-auto-animate>
                <InfoBlock  
                    v-if="!totalPrice && !orderId"                  
                    title="Корзина пуста" 
                    desc="Выберирте товар на странице!" 
                    url-image="./../public/package-icon.png"
                />
                <InfoBlock           
                    v-if="orderId"         
                    title="Заказ оформлен" 
                    :desc="`Ваш заказ №${orderId} передан в обработку`"
                    url-image="./../public/order-success-icon.png"
                />
            </div>
            <DraverFooter
                v-if="totalPrice"
                :total-price="totalPrice"
                :vat-price="vatPrice"
                @creat-order="creatOrder"
            />
        </div>
    </aside>
</template>