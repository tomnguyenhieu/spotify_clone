<script setup>
import { ref, computed, onMounted } from "vue";
import { Icon } from '@iconify/vue';
import { useViewStore } from "@/stores/view";
import { storeToRefs } from "pinia";
import { useSongStore } from "@/stores/song";
import { useAuthStore } from '@/stores/auth';
import axios from 'axios';

const useView = useViewStore();
const authStore = useAuthStore();
const useSong = useSongStore();


onMounted(() => {
    console.log(authStore.user)
})
</script>

<template>
    <div class="text-white space-y-10 rounded-[24px] bg-[#1D1512] w-full h-[76%]">
        <div class="px-10 py-6 h-52 flex items-center bg-gradient-to-b from-[#1D1512]/20 to-[#312825]/100 space-x-7 ">
            <div class="rounded-full bg-gray-600 w-[160px] h-[160px]">
                <img class="" :src="authStore.user.avatar" alt="">
            </div>
            <div class="space-y-2">
                <p class="text-lg text-zinc-400">Hồ sơ</p>
                <h1 class="text-6xl font-bold">{{ authStore.user.name }}</h1>
                <p class="mt-1 text-lg text-zinc-400">? Playlist công khai • ??? đang theo dõi</p>
            </div>
        </div>
        
        <div class="px-10 overflow-auto scrollbar-style h-[calc(100vh-450px)]">
            <button class="text-zinc-400 text-3xl mb-5 p-2 rounded-full hover:bg-zinc-600 hover:text-white">
                <Icon icon="ph:dots-three-outline-fill"/>
            </button>
            <div>
                <h2 class="mb-4 text-lg font-semibold">Playlist công khai</h2>
                <div class="flex overflow-x-auto space-x-7 scrollbar-style">
                    <div v-for="i in 3" :key="i" class="flex-shrink-0 w-32">
                        <div class="w-full h-32 mb-2 rounded bg-zinc-700">
                        </div>
                        <p class="font-medium">Playlist#{{ i }}</p>
                        <p class="text-sm text-zinc-400">{{ i * 100 }} người theo dõi</p>
                    </div>
                </div>
            </div>

            <div class="mt-8">
                <h2 class="mb-4 text-lg font-semibold">Đang theo dõi</h2>
                <div class="flex overflow-x-auto space-x-7 scrollbar-style">
                    <div v-for="i in 4" :key="i" class="flex-shrink-0">
                        <div class="w-32 h-32 mb-5 rounded-full bg-zinc-700">
                        </div>
                        <p class="text-sm text-zinc-400"> Ca sĩ {{ i }}</p>

                    </div>

                </div>
            </div>

            <div class="mt-8">
                <h2 class="mb-4 text-lg font-semibold">Danh sách phát</h2>
                <div class="flex overflow-x-auto space-x-7 scrollbar-style">
                    <div v-for="i in 3" :key="i" class="flex-shrink-0 w-32 ">
                        <div class="w-full h-32 mb-2 rounded bg-zinc-700">


                        </div>
                        <p class="font-medium">Playlist#{{ i }}</p>
                        <p class="text-sm text-zinc-400">{{ i * 100 }} người theo dõi</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
.scrollbar-style {
    scrollbar-width: medium;
    scrollbar-color: #BC4D15 transparent;
}
</style>