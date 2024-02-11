
<template>
    <div class="flex flex-col height-auto relative border rounded-[40px] pt-5 px-7 pb-8 cursor-pointer hover:shadow-2xl duration-500">
        <img class='lazy absolute' width='32' height='32' src='/like-1.svg' alt='Иконка сердечка'>
        <img class='lazy mb-2' width='133' height='112' src='/sneakers/sneakers-1.jpg' alt='Изображение кроссовок'>
        <h6 class="mb-2 text-sm text-wrap">Мужские Кроссовки Nike Blazer Mid Suede</h6>
        <slot></slot>
        <div class="flex align-center justify-between mt-auto">
            <div class="flex flex-col">
                <span class="text-slate-400 text-xs">цена</span>
                <span class="font-bold text-sm">12 999 руб.</span>
            </div>
            <button>
                <img class='' width='32' height='32' src='/plus.svg' title='Кнопка плюс'>
            </button>
        </div>
    </div>
</template>