<script setup>
    import { inject } from 'vue';
    import DraverHeader  from './DriverHeader.vue';
    import CartItemList from './CartItemList.vue'
    import DraverFooter from './DraverFooter.vue'
    import InfoBlock from './InfoBlock.vue';
    const {totalPrice, vatPrice, creatOrder} = inject('cartActions')
    const emit = defineEmits(['closeDriver'])
</script>

<template>
    <div @click="()=>emit('closeDriver')" class="fixed top-0 left-0 w-screen h-screen bg-black z-10 opacity-50" v-auto-animate></div>
    <aside class="fixed  top-0 right-0 max-w-[420px] size-full h-screen bg-white z-20" v-auto-animate>
        <div class="p-10 flex flex-col h-full">
            <DraverHeader/>
            <CartItemList  />
            <InfoBlock 
                v-if="!totalPrice"
                title="Корзина пуста" 
                desc="Выберирте товар на странице!" 
                url-image="./../public/package-icon.png"
            />
            <DraverFooter
                v-if="totalPrice"
                :total-price="totalPrice"
                :vat-price="vatPrice"
                @creat-order="creatOrder"
            />
        </div>
    </aside>
</template>