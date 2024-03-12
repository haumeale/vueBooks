<script setup>
import { onMounted, ref , reactive, watch } from 'vue'
import axios from 'axios'

import HeaderVue from './components/HeaderVue.vue'
import CardList from './components/CardList.vue'
import DrawerVue from './components/DrawerVue.vue';

const items = ref([])

const filters = reactive({
    sortBy: 'title',
    searchQuerry: ''
})

const onChangeSelect = (event) => {
    filters.sortBy = event.target.value
}

const onChangeSearch = (event) => {
    filters.searchQuerry = event.target.value
}

const fetchItems = async () => {
    try {

        const params =  {
            sortBy: filters.sortBy
        }

        if (filters.searchQuerry){
            params.title = `*${filters.searchQuerry}*`
        }
        const { data } = await axios.get('https://f4a0b45a3cfbddec.mokky.dev/items', {
            params
        })
        items.value = data
    } catch (err) {
        console.log(err)
    }
}

onMounted(fetchItems)
watch(filters, fetchItems)
        
</script>
 
<template>
    <div class="bg-[#ddd6fe] w-4/5 m-auto h-full rounded-xl shadow-xl mt-14">
    <!-- <DrawerVue /> -->
    <HeaderVue/>

    <div class="p-10">
        <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">All books</h2>

           <div class="flex gap-5">
        <select @change="onChangeSelect" class="py-2 px-3 border rounded-md focus:border-violet-300 outline-none bg-[#ddd6fe]">
            <option value="name">By name</option>
        </select>
        <div class="relative">
            <img class="absolute left-4 top-3" src="/src/assets/search.svg" alt="">
            <input
            @input="onChangeSearch"
             class="border rounded-md py-2 pl-12 pr-4 outline-none bg-violet-200 focus:border-violet-300" placeholder="Search...">
        </div>
        </div>
        </div>
        
    <CardList :items="items"/>
      
    </div>
    </div>
</template>



<style scoped>

</style>