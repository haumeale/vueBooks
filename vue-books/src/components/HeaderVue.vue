<template>
    <header class="flex justify-between border-b border-violet-700 px-10 py-8">
    <div class="flex items-center gap-4">
    <img src="/src/assets/book3.png" alt="" class="w-11">
    <div>
        <h2 class="text-xl font-bold">Vue Books</h2>
        <p class="text-slate-600">The best book store</p>
    </div>
    </div>

    <ul class="flex items-center gap-10">
    <li class="flex items-center gap-3 text-gray-600 hover:text-black cursor-pointer">
    <img src="/src/assets/cart.svg" alt=""> 
    <b>2345 rub.</b>
           
    </li>

    <li class="flex items-center gap-3 text-gray-600 hover:text-black cursor-pointer">
    <img src="/src/assets/heart.svg" alt=""> 
    <span>Favorites</span>
           
    </li>

    <li class="flex items-center gap-3 text-gray-600 hover:text-black cursor-pointer">
    <img src="/src/assets/profile.svg" alt=""> 
    <span>Profile</span>
           
    </li>
    </ul>
    </header>
    
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>

</style>