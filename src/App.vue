<script setup>
import { ref } from "vue";

const jumps = ref(0);
const isLeftPosition = ref(true);
const isJumping = ref(false);
const sheepSprite = ref("/Sheep_sleep.png");

const toggleDirection = () => {
    isLeftPosition.value = !isLeftPosition.value;
    sheepSprite.value = "/Sheep_stand.png";
    jumps.value++;
};
</script>

<template>
    <div
        class="h-screen flex flex-col justify-center items-center gap-6 bg-slate-50 overflow-hidden"
    >
        <h1 class="text-4xl font-bold select-none">{{ jumps }}</h1>

        <div class="relative w-full h-[500px]">
            <div
                class="absolute left-1/2 top-[100px] -ml-16 origin-[64px_800px] transition-transform duration-3000 ease-in-out"
                :class="isLeftPosition ? 'rotate-[-55deg]' : 'rotate-[55deg]'"
            >
                <img
                    @click="toggleDirection"
                    class="w-32 h-32 cursor-pointer object-cover hover:scale-105 transition-transform duration-3000 ease-in-out"
                    :class="
                        isLeftPosition ? 'rotate-[55deg]' : 'rotate-[-55deg]'
                    "
                    :src="sheepSprite"
                    alt="Jumping Sheep"
                />
            </div>
        </div>
    </div>
</template>
