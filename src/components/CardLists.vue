<script setup>
import Card from './Card.vue';

</script>

<template>
    <div class="grid auto-fit   gap-8">	
        <Card/>
        <Card/>        
        <Card/>
        <Card/>
    </div>
</template>

<style scoped>
.auto-fit {    
    grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
}
</style>