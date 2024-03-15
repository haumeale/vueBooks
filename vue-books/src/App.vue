<script setup>
import { onMounted, ref , reactive, provide, watch, computed } from 'vue'
import axios from 'axios'

import HeaderVue from './components/HeaderVue.vue'
import CardList from './components/CardList.vue'
import DrawerVue from './components/DrawerVue.vue';

const items = ref([])
const cart = ref([])

const isCreatingOrder = ref(false)

const drawerOpen = ref(false)

const totalPrice = computed(
    () => cart.value.reduce((acc, item) => acc + item.price, 0)
)

const cartIsEmpty = computed(() => cart.value.length === 0)

const cartButtonDisable = computed(() => 
isCreatingOrder.value || cartIsEmpty.value)

const closeDrawer = () => {
    drawerOpen.value = false
}

const openDrawer = () => {
    drawerOpen.value = true
}

const filters = reactive({
    sortBy: 'title',
    searchQuerry: ''
})

const addToCart = (item) => {
    cart.value.push(item)
        item.isAdded = true
}

const removeFromCart = (item) => {
    cart.value.splice(cart.value.indexOf(item), 1)
        item.isAdded = false
}

const createOrder = async () =>  {
try {
    const { data } = await axios.post(`https://f4a0b45a3cfbddec.mokky.dev/orders`, {
        items: cart.value,
        totalPrice: totalPrice.value,

    })
    cart.value = []
    return data
}  catch (err){
    console.log(err)

} finally {
    isCreatingOrder.value = false
}
}

const onClickAddPlus = (item) => {
    if (!item.isAdded) {
       addToCart(item)
    } else {
       removeFromCart(item)
        
    }
}


const onChangeSelect = (event) => {
    filters.sortBy = event.target.value
}

const onChangeSearch = (event) => {
    filters.searchQuerry = event.target.value
}

const fetchFavorites = async () => {
    try {
const { data: favorites } = await axios.get(`https://f4a0b45a3cfbddec.mokky.dev/favorites`)
items.value = items.value.map(item => {
    const favorite = favorites.find(favorite => favorite.parentId === item.id)
    if(!favorite) {
        return item
    }

    return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id,
    }
})
} catch (err) {
console.log(err)
}
}

const addToFavorite = async (item) => {
    try{

        if(!item.isFavorite) {
            const obj = {
                parentId: item.id

            }
            item.isFavorite = true
            
            const { data } = await axios.post(`https://f4a0b45a3cfbddec.mokky.dev/favorites`, obj)

            item.favoriteId = data.id
        }     else {
            item.isFavorite = false
            await axios.delete(`https://f4a0b45a3cfbddec.mokky.dev/favorites/${item.favoriteId}`)
            item.favoriteId = null
        } 
            
    } catch (err) {
        console.log(err)
    }
    }

const fetchItems = async () => {
    try {

        const params =  {
            sortBy: filters.sortBy
        }

        if (filters.searchQuerry){
            params.title = `*${filters.searchQuerry}*`
        }
        const { data } = await axios.get(`https://f4a0b45a3cfbddec.mokky.dev/items`, {
            params
        })
        items.value = data.map(obj => ({
            ...obj,
            isFavorite: false,
            favoriteId: null,
            isAdded: false
        }))
    } catch (err) {
        console.log(err)
    }
}

onMounted( async () => {
   await fetchItems();
   await fetchFavorites();
}
)
watch(filters, fetchItems)

watch(cart, () => {
    items.value = items.value.map((item) => ({
        ...item,
        isAdded: false
    }))
})

provide('cart', {
    cart,
    closeDrawer,
    openDrawer,
    addToCart,
    removeFromCart
})
        
</script>
 
<template>
    <DrawerVue v-if="drawerOpen" :total-price="totalPrice" @create-order="createOrder" :button-disable="cartButtonDisable"/>
    <div class="bg-[#ede9fe] w-4/5 m-auto min-h-screen rounded-xl shadow-xl mt-14">
    <HeaderVue :total-price="totalPrice" @open-drawer="openDrawer" />

    <div class="p-10">
        <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">All books</h2>

           <div class="flex gap-5">
        <select @change="onChangeSelect" class="py-2 px-3 border rounded-md focus:border-violet-300 outline-none bg-violet-100">
            <option value="name">By name</option>
        </select>
        <div class="relative">
            <img class="absolute left-4 top-3" src="/src/assets/search.svg" alt="">
            <input
            @input="onChangeSearch"
             class="border rounded-md py-2 pl-12 pr-4 outline-none bg-violet-100 focus:border-violet-300" placeholder="Search...">
        </div>
        </div>
        </div>
        
    <CardList :items="items" @add-to-favorite="addToFavorite" @add-to-cart="onClickAddPlus"/>
      
    </div>
    </div>
</template>



<style scoped>

</style>