<script setup>
const emit = defineEmits(['onClickRemove'])

defineProps({
    id: Number,
    title: String,
    imageUrl: String,
    price: Number,
    
})
</script>

<template>
   <div class=" flex items-center border border-violet-300 p-4 rounded-xl gap-4">
    <img class="w-16 h-16" :src="imageUrl" :alt="title">
    <div class="flex flex-col">
        <p>{{ title }}</p>
        <div class="flex justify-between mt-2">
            <b>{{ price }} rub.</b>
            <img @click="emit('onClickRemove')" class="opacity-50 hover:opacity-100 cursor-pointer transition" src="/src/assets/close.svg" alt="">
        </div>
    </div>
   </div>
</template>