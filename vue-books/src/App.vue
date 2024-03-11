<script setup>
import HeaderVue from './components/HeaderVue.vue'
import CardList from './components/CardList.vue'
        
</script>
 
<template>
<div class="w-4/5 m-auto bg-[#ddd6fe] h-screen rounded-xl shadow-xl mt-14">
    <HeaderVue/>

    <div class="p-10">
    <h2 class="text-3xl font-bold mb-8">All books</h2>

    <CardList />
    </div>
    </div>
</template>



<style scoped>

</style>