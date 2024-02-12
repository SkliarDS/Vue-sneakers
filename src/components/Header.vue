<script setup>

</script>



<template>
    <header class="header flex justify-between items-center p-10 border-b">
        <a href="/" class="flex items-center gap-x-1.5">
            <img class="lazy" width='80' height='80' src='/logo.png' alt='Logo' title='Logo'>
            <div class="">
                <h2 class="text-xl font-bold uppercase">SNEAKERS</h2>
                <span class="text-slate-500">Магазин лучших кроссовок</span>
            </div>
        </a>
        <nav>
            <ul class="flex items-center gap-x-8">
                <li class="flex items-center gap-x-1.5 cursor-pointer text-slate-500 hover:text-black">
                    <img class='lazy' width='20' height='20' src='/cart.svg' alt='Иконка корзины' title='Иконка корзины'>
                    <span><b>1205 руб.</b></span>
                </li>
                <li class="flex items-center gap-x-1.5 cursor-pointer text-slate-500 hover:text-black">
                    <img class=' lazy' width='20' height='20' src='/heart.svg' alt='Иконка сердца' title='Иконка сердца'>
                    <span>Закладки</span>
                </li>
                <li class="flex items-center gap-x-1.5 cursor-pointer text-slate-500 hover:text-black">
                    <img class=' lazy' width='20' height='20' src='/profile.svg' alt='Иконка профиля' title='Иконка профиля'>
                    <span>Профиль</span>
                </li>
            </ul>
        </nav>
    </header>
</template>

<style>
</style>
