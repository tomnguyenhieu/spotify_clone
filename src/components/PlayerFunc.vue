<script setup>
import { ref, watch, onMounted } from "vue";
import { Icon } from '@iconify/vue';
import { useSongStore } from "@/stores/song";
import { useViewStore } from "@/stores/view";
import { storeToRefs } from "pinia";

const useSong = useSongStore();
const useView = useViewStore();
const { audio } = storeToRefs(useSong);

let isHover = ref(false);
let vol = ref(80);
let volume = ref(null);

onMounted(() => {
  volume.value.addEventListener('input', (e) => {
    audio.value.volume = e.currentTarget.value / 100;
  });
  useView.listenFullscreenChange();
})

</script>

<template>
  <Icon icon="ic:round-volume-off" v-if="vol == 0" class=" text-white size-7"/>
  <Icon icon="ic:round-volume-up" v-else class=" text-white size-7"/>
  <div class="flex items-center ml-2 w-[150px] relative mt-2 mb-[23px]" @mouseenter="isHover = true"
    @mouseleave="isHover = false">
    <input v-model="vol" ref="volume" type="range"
      class="mt-[24px] absolute rounded-full my-2 w-full h-0 z-40 appearance-none bg-opacity-100 focus:outline-none accent-white" />
    <div class="pointer-events-none mt-[6px] absolute h-[4px] z-10 inset-y-0 left-0 w-0" :style="'width: ${vol}%;'"
      :class="isHover ? 'bg-green-500' : 'bg-white'"></div>
    <div class="absolute h-[4px] z-[-0] mt-[6px] inset-y-0 left-0 w-full bg-gray-500 rounded-full"></div>
  </div>
  <div class=" ml-4" >
    <Icon icon="fa6-solid:compress" v-if="useView.isFullscreen"  class="text-white size-6 cursor-pointer" @click="useView.toggleFullscreen"/>
    
    <Icon icon="fa6-solid:expand" v-else class="text-white size-6 cursor-pointer text-semibold" @click="useView.toggleFullscreen"/>
  </div>
</template>
