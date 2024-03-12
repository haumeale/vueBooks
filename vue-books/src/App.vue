<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

import HeaderVue from './components/HeaderVue.vue'
import CardList from './components/CardList.vue'
import DrawerVue from './components/DrawerVue.vue';

const items = ref([])



onMounted( async () => {
    try {
        const { data } = await axios.get('https://f4a0b45a3cfbddec.mokky.dev/items')
        items.value = data
    } catch (err) {
        console.log(err)
    }
})
        
</script>
 
<template>
    <div class="w-4/5 m-auto bg-[#ddd6fe] h-full rounded-xl shadow-xl mt-14">
    <!-- <DrawerVue /> -->
    <HeaderVue/>

    <div class="p-10">
        <div class="flex justify-between">
        <h2 class="text-3xl font-bold mb-8">All books</h2>
        <div class="relative">
            <img class="absolute left-4 top-3" src="/src/assets/search.svg" alt="">
            <input
            
             class="border rounded-md py-2 pl-12 pr-4 outline-none bg-violet-200 focus:border-violet-300" placeholder="Search...">
        </div>
        </div>
        
    <CardList :items="items"/>
      
    </div>
    </div>
</template>



<style scoped>

</style>