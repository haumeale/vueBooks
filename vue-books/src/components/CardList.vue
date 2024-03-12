<script setup>
import CardVue from './CardVue.vue';

defineProps({
    items: Array
})

const onClickAdd = () => {
    alert('You have added an item to your cart!')
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
        :onClickAdd="onClickAdd"
        />
       

    </div>
</template>