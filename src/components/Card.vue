<script setup>
    defineProps({
        imageUrl: String,
        title: String,
        price: Number,
        isFavorite: Boolean,
        isAdded: Boolean,
        onClickAdd: Function,
        onClickFavorite: Function
    })
    
</script>
<template>
    <div class="flex flex-col ht-auto relative border rounded-[40px] pt-5 px-7 pb-8 cursor-pointer hover:shadow-2xl duration-500 ">
        <img class='lazy absolute' 
            width='32' height='32' 
            @click="onClickFavorite" 
            :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'" 
            alt='Иконка сердечка'
        >
        <img class='lazy mb-2' width='133' height='112' :src='imageUrl' alt='Изображение кроссовок'>
        <h6 class="mb-2 text-sm text-wrap">{{ title }}</h6>
        <div class="flex align-center justify-between mt-auto">
            <div class="flex flex-col">
                <span class="text-slate-400 text-xs">цена</span>
                <span class="font-bold text-sm"><b>{{ price }}</b> руб.</span>
            </div>
            <button @click="onClickAdd">
                <img class='' width='32' height='32' :src="!isAdded ? '/plus.svg' : '/checked.svg'" title='Кнопка плюс'>
            </button>
        </div>
    </div>
</template>