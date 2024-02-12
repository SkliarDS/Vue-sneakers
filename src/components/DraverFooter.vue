<script setup>

</script>
<template>
    <div class="grid gap-y-5 mt-auto">
        <div class="flex justify-between bg-dots">
            <span class="text-sm text-wrap">Итого</span>
            <span class="font-bold text-sm">21 400 руб.</span>
        </div>
        <div class="flex justify-between bg-dots">
            <span class=" text-sm text-wrap">Налог 5%: </span>
            <span class="font-bold text-sm">1 400 руб.</span>
        </div>
        <button class="flex items-center justify-center gap-x-3 py-3 px-10 text-white rounded-xl hover:shadow-md duration-500">
            Оформить заказ
            <svg class="hover:opacity-70 duration-300" width="16" height="14" viewBox="0 0 16 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M1 7H14.7143" stroke="#FFFFFF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M8.71436 1L14.7144 7L8.71436 13" stroke="#FFFFFF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
        </button>
    </div>
</template>

<style scoped>
    button {
        background: rgb(157, 213, 88);
    }
    .bg-dots {
        position: relative;

    }
    .bg-dots::before {
        position: absolute;
        content: '';
        border: 0.5px dashed #ebe9e9;
        width: 100%;
        height: 2px;
        left: 0;
        bottom: 5px;
        
    }
    .bg-dots span {
        position: relative;
        background: white;
        padding: 0 5px;
    }
</style>