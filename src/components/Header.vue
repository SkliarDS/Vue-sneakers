<script setup>
defineProps ({
    totalPrice: Number,
    countCart: Number,
    // counFavorite: Number
})
    const emit = defineEmits(['openDriver']) 
</script>



<template>
    <header class="header flex justify-between items-center p-10 border-b">
        <router-link to="/">
            <div class="flex items-center gap-x-1.5">
                <img class="lazy" width='80' height='80' src='/logo.png' alt='Logo' title='Logo'>
                <div class="">
                    <h2 class="text-xl font-bold uppercase">SNEAKERS</h2>
                    <span class="text-slate-500">Магазин лучших кроссовок</span>
                </div>
            </div>
        </router-link>
        <nav>
            <ul class="flex items-center gap-x-8">
                <li @click="()=>emit('openDriver')" class="flex items-center gap-x-1.5 cursor-pointer text-slate-500 hover:text-black relative">
                    <span class="flex items-center justify-center absolute w-[20px] h-[20px] bg-slate-300 rounded-full text-white -top-4">{{ countCart }}</span>
                    <img class='lazy' width='20' height='20' src='/cart.svg' alt='Иконка корзины' title='Иконка корзины'>
                    <span><b>{{ totalPrice }} руб.</b></span>
                </li>
                <li>
                    <router-link to="/favorites">
                        <div class="flex items-center gap-x-1.5 cursor-pointer text-slate-500 hover:text-black relative">
                            <span></span>
                            <img class=' lazy' width='20' height='20' src='/heart.svg' alt='Иконка сердца' title='Иконка сердца'>
                            <span>Закладки</span>
                        </div>
                    </router-link>
                </li>
                <li>
                    <router-link to="/profile">
                        <div class="flex items-center gap-x-1.5 cursor-pointer text-slate-500 hover:text-black">
                            <img class=' lazy' width='20' height='20' src='/profile.svg' alt='Иконка профиля' title='Иконка профиля'>
                            <span>Профиль</span>
                        </div>
                    </router-link>
                </li>
            </ul>
        </nav>
    </header>
</template>

<style>
</style>
