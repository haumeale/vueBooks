<script setup>
import CardVue from './CardVue.vue';

defineProps({
    items: Array,  
})

const emit = defineEmits(['addToFavorite'])

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
        :onClickAdd="onClickAdd"
        :isFavorite="item.isFavorite"
        :onClickFavorite="() => emit('addToFavorite', item)"
        />
       

    </div>
</template>