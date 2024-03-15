 <script setup>
 import DrawerHead from './DrawerHead.vue';
 import CartItemList from './CartItemList.vue';

 const emit = defineEmits(['createOrder'])

 defineProps({
    totalPrice: Number,
    buttonDisable: Boolean
 })

</script>
 
 <template>
    <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
    <div class="bg-[#ddd6fe] w-96 h-full fixed right-0 top-0 z-20 p-8">
        <DrawerHead />
        <CartItemList />

        <div class="flex flex-col gap-4 mb-6 mt-7">
            <div class="flex gap-2">
                <span>Sum total</span>
                <div class="flex-1 border-b border-dashed" ></div>
                <b>{{ totalPrice }} ₽</b>
            </div>
            <button
            @click="() => emit('createOrder')"
        :disabled="buttonDisable"
         class="bg-violet-400 w-full disabled:bg-violet-300 rounded-xl py-3 text-white hover:bg-violet-500 active:bg-violet-600 transition cursor-pointer">
            Place an order
        </button>
        </div>

       
        
    </div>
</template>