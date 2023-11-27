<script setup>
    import { ref, reactive, onMounted } from 'vue'


    let message = ref("Heyy");
    let allMessages = reactive({
        data: ["Heyy", "Hoi", "Hallo"],
    });

    // function sendMessage
    const sendMessage = () => {
        allMessages.data.push(message.value);
        message.value = "";
    };

</script>

<template>
  <div>
    <ul>
        <li v-for="m in allMessages.data">{{ m }}</li>
    </ul>

    <div>
        <input @keyup.enter="sendMessage" v-model="message" type="text" placeholder="">
        <button @click="sendMessage">Send</button>
    </div>
  </div>
</template>

<style scoped>

</style>
