<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import GetTiktok from './getTiktok.vue';

const idProfile = "UCa9hJEqPBtZGRFJg7gYMhdg";
const url = `https://decapi.me/youtube/latest_video?id=${idProfile}&format={"id":"{id}","title":"{title}"}&no_livestream=1`;
const urlPicture = ref('');
const urlVideo = ref('');
const data = ref<{ id: string, title: string } | null>(null);

async function getVideo() {
    try {
        const response = await fetch(url);
        const result = await response.json();

        data.value = result;
        
        if (data.value) {
            urlPicture.value = `https://i.ytimg.com/vi/${data.value.id}/hqdefault.jpg`;
            urlVideo.value = `https://www.youtube.com/watch?v=${data.value.id}`;
        }
    } catch (error) {
        console.error('Error fetching video data:', error);
    }
}

onMounted(() => {
    getVideo();
});
</script>

<template>
<section class="w-[450px]">
    <div class="flex justify-center">
        <img class="rounded-full mt-8" src="/profile_pic.jpg" alt="Pedereando">
    </div>
    <h1 class="mt-1 text-center text-4xl font-bold">Pedereando<br>Podcast</h1>
    <div class="flex justify-center">
        <div class="mt-4 flex justify-between w-[300px]">
            <a href="https://www.tiktok.com/@pedereando.podcast" target="_blank">
                <svg class="hover:text-[#53469b] transition-all" width="64" height="64" fill="currentColor" viewBox="0 0 256 256">
                    <path d="M224,72a48.05,48.05,0,0,1-48-48,8,8,0,0,0-8-8H128a8,8,0,0,0-8,8V156a20,20,0,1,1-28.57-18.08A8,8,0,0,0,96,130.69V88a8,8,0,0,0-9.4-7.88C50.91,86.48,24,119.1,24,156a76,76,0,0,0,152,0V116.29A103.25,103.25,0,0,0,224,128a8,8,0,0,0,8-8V80A8,8,0,0,0,224,72Zm-8,39.64a87.19,87.19,0,0,1-43.33-16.15A8,8,0,0,0,160,102v54a60,60,0,0,1-120,0c0-25.9,16.64-49.13,40-57.6v27.67A36,36,0,1,0,136,156V32h24.5A64.14,64.14,0,0,0,216,87.5Z"></path>
                </svg>
            </a>
            <a href="https://www.instagram.com/pedereando/" target="_blank">
                <svg class="hover:text-[#53469b] transition-all" width="64" height="64" fill="currentColor" viewBox="0 0 256 256">
                    <path d="M128,80a48,48,0,1,0,48,48A48.05,48.05,0,0,0,128,80Zm0,80a32,32,0,1,1,32-32A32,32,0,0,1,128,160ZM176,24H80A56.06,56.06,0,0,0,24,80v96a56.06,56.06,0,0,0,56,56h96a56.06,56.06,0,0,0,56-56V80A56.06,56.06,0,0,0,176,24Zm40,152a40,40,0,0,1-40,40H80a40,40,0,0,1-40-40V80A40,40,0,0,1,80,40h96a40,40,0,0,1,40,40ZM192,76a12,12,0,1,1-12-12A12,12,0,0,1,192,76Z"></path>
                </svg>
            </a>
            <a href="https://www.youtube.com/@Pedereando" target="_blank">
                <svg class="hover:text-[#53469b] transition-all" width="64" height="64" fill="currentColor" viewBox="0 0 256 256">
                    <path d="M164.44,121.34l-48-32A8,8,0,0,0,104,96v64a8,8,0,0,0,12.44,6.66l48-32a8,8,0,0,0,0-13.32ZM120,145.05V111l25.58,17ZM234.33,69.52a24,24,0,0,0-14.49-16.4C185.56,39.88,131,40,128,40s-57.56-.12-91.84,13.12a24,24,0,0,0-14.49,16.4C19.08,79.5,16,97.74,16,128s3.08,48.5,5.67,58.48a24,24,0,0,0,14.49,16.41C69,215.56,120.4,216,127.34,216h1.32c6.94,0,58.37-.44,91.18-13.11a24,24,0,0,0,14.49-16.41c2.59-10,5.67-28.22,5.67-58.48S236.92,79.5,234.33,69.52Zm-15.49,113a8,8,0,0,1-4.77,5.49c-31.65,12.22-85.48,12-86,12H128c-.54,0-54.33.2-86-12a8,8,0,0,1-4.77-5.49C34.8,173.39,32,156.57,32,128s2.8-45.39,5.16-54.47A8,8,0,0,1,41.93,68c30.52-11.79,81.66-12,85.85-12h.27c.54,0,54.38-.18,86,12a8,8,0,0,1,4.77,5.49C221.2,82.61,224,99.43,224,128S221.2,173.39,218.84,182.47Z"></path>
                </svg>
            </a>
        </div>
    </div>

    <h2 class="my-4 text-center text-3xl font-bold">Ultimo video</h2>
    
    <div class="mx-4 border-2 hover:border-[#53469b] hover:scale-105 transition-all rounded-lg">
        <a :href="urlVideo" target="_blank">
            <div class="relative w-full h-0 pb-[55.90%]">
                <img class="absolute top-0 left-0 w-full h-full object-cover object-center rounded-lg" :src="urlPicture" :alt="data?.title || 'Video Thumbnail'">
            </div>
        </a>
    </div>
    <div class="grid gap-4 my-8 justify-center">
        <GetTiktok/>
    </div>

</section>
</template>
