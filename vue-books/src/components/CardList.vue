<script setup>
import CardVue from './CardVue.vue';

const onClickAdd = () => {
    alert('You have added an item to your cart!')
}

</script>

<template>
    <div class="grid grid-cols-4 gap-5">
        <CardVue title="Фрэнсис Бёрнетт: Таинственный сад" 
        imageUrl="/src/assets/books1.jpeg" 
        :price="888" 
        :is-added="true" 
        :isFavorite="true" 
        :onClickAdd="onClickAdd"
        />
        <CardVue />
        <CardVue />
        <CardVue />
        <CardVue />
        <CardVue />
        <CardVue />
        <CardVue />

    </div>
</template>