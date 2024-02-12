<script setup>
    defineProps({
        imageUrl: String,
        title: String,
        price: Number,
        onRemove: Function
    })
</script>
<template>
    <article class="flex justify-between gap-x-3 border rounded-[40px] p-5 cursor-pointer hover:shadow-md duration-500">
        <img class='lazy flex-shrink-0 w-20 h-20' width='70' height='70' :src='imageUrl' title='Изображение кроссовок'>
        <div class="flex flex-col">
            <h6 class="mb-2 text-sm text-wrap">{{ title }}</h6>
            <span class="font-bold text-sm">{{ price }}</span>
        </div>
        <button type="button" class="mt-auto opacity-50 hover:opacity-100 duration-300">
            <img class='' width='32' height='32' src='/close.svg' title='Иконка закрыть'>
        </button>
    </article>
</template>