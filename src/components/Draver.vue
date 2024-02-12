<script setup>
    import DraverHeader  from './DriverHeader.vue';
    import CartItemList from './CartItemList.vue'
    import DraverFooter from './DraverFooter.vue'
</script>

<template>
    <div class="fixed top-0 left-0 w-screen h-screen bg-black z-10 opacity-50"></div>
    <aside class="fixed  top-0 right-0 max-w-[420px] size-full h-screen bg-white z-20 ">
        <div class="p-10 flex flex-col h-full">
            <DraverHeader/>
            <CartItemList/>
            <DraverFooter/>
        </div>
    </aside>
</template>