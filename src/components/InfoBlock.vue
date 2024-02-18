<script setup>
    defineProps({
        urlImage: String,
        title: String,
        desc: String
    })
</script>

<template>
    <div class="flex items-center  justify-center w-full h-full" v-auto-animate>
        <div class="flex flex-col items-center gap-2 w-100">
            <img class='' width='70' height='70' :src='urlImage' title=''>
            <h5 class="font-semibold text-2xl">{{ title }}</h5>
            <p class="color-gray-400 text-center">{{ desc }}</p>
        </div>
    </div>
</template>