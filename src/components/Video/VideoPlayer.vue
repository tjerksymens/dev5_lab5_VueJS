<script setup>
import { ref, reactive, onMounted } from 'vue'

//define emit
const emit = defineEmits(["update:videoDescription"]);


let videoUrl = ref("");
let videos = reactive({
    data: [],
});

onMounted(() => {
    fetch("https://api.jsonbin.io/v3/b/6548ef9954105e766fcc2c15")
        .then((res) => res.json())
        .then((data) => {
            console.log(data.record);
            videos.data = data.record.videos;
            videoUrl.value = videos.data[0].video;

            //emit
            emit("update:videoDescription", videos.data[0].description);
        });
});


</script>

<template>
    <div>
        <video :src="videoUrl" controls autoplay muted loop></video>
    </div>
</template>

<style scoped>

</style>
