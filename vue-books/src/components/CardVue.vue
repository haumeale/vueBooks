<script setup>
defineProps({
    id: Number,
    imageUrl: String,
    title: String,
    price: Number,
    isFavorite: Boolean,
    isAdded: Boolean,
    onClickAdd: Function,
    onClickFavorite: Function
})


</script>


<template>
     <div class="relative bg-[#ede9fe] border border-violet-200 rounded-3xl p-8 pb-4 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
        <img :src="!isFavorite ? '/src/assets/like-1.svg' : '/src/assets/like-2.svg' " alt="" class="absolute top-8 left-8 " @click="onClickFavorite">
        <img :src="imageUrl" alt="">
        <p class="mt-2">{{ title }}</p>
        <div class="flex justify-between mt-2">
            <div class="flex flex-col">
                <span class="text-violet-400">Price:</span>
                <b>{{ price }} rub.</b>
            </div>
            <img :src="!isAdded ? '/src/assets/plus.svg' : '/src/assets/checked.svg'" alt="" @click="onClickAdd">

        </div>

      </div>
</template>