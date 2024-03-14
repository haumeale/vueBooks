<script setup>
import CardVue from './CardVue.vue';

defineProps({
    items: Array,  
})

const emit = defineEmits(['addToFavorite', 'addToCart'])

const onClickAdd = () => {
    alert('You have added an item to your cart!')
    emit('addToFavorite', item)
}

</script>

<template>
    <div class="grid grid-cols-4 gap-5 mt-4">
        <CardVue
        v-for="item in items"
        :key="item.id"
         :title="item.title" 
        :imageUrl="item.imageUrl" 
        :price="item.price" 
        :id="item.id"
        :isFavorite="item.isFavorite"
        :onClickFavorite="() => emit('addToFavorite', item)"
        :onClickAdd="() => emit('addToCart', item)"
        :isAdded="item.isAdded"
        />
       

    </div>
</template>