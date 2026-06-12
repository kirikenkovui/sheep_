<script setup>
import { ref } from "vue";

const jumps = ref(0);
const isLeftPosition = ref(true);
const isJumping = ref(false);

import backgroundImg from "./Sheep_background.webp";
import sheepStandImg from "./Sheep_stand.png";
import sheepSleepImg from "./Sheep_sleep.png";

const sheepSprite = ref(sheepSleepImg);

const toggleDirection = () => {
    if (isJumping.value) {
        return;
    }
    isJumping.value = true;
    isLeftPosition.value = !isLeftPosition.value;
    sheepSprite.value = sheepStandImg;
    jumps.value++;

    setTimeout(() => {
        isJumping.value = false;
        sheepSprite.value = sheepSleepImg;
    }, 3000);
};
</script>

<template>
    <div
        class="h-screen w-screen flex flex-col justify-center items-center gap-6 bg-slate-50 bg-cover bg-center bg-no-repeat overflow-hidden"
        :style="{ backgroundImage: `url(${backgroundImg})` }"
    >
        <h1 class="text-8xl font-bold select-none text-white">{{ jumps }}</h1>

        <div class="relative w-full h-125">
            <div
                class="absolute left-1/2 top-25 -ml-16 origin-[64px_800px] transition-transform duration-3000 ease-in-out"
                :class="isLeftPosition ? 'rotate-[-55deg]' : 'rotate-55'"
            >
                <img
                    @click="toggleDirection"
                    class="w-48 h-48 cursor-pointer object-cover transition-transform duration-3000 ease-in-out"
                    :class="[
                        isLeftPosition
                            ? 'rotate-[-55deg] scale-x-[-1]'
                            : 'rotate-55 scale-x-100',
                    ]"
                    :src="sheepSprite"
                    alt="Jumping Sheep"
                />
            </div>
        </div>
    </div>
</template>
