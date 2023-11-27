<script setup>
    import { ref, reactive, onMounted } from 'vue'

    let message = ref("Heyy");
    let allMessages = reactive({
        data: [],
    });

    // function to fetch messages from the API
    const fetchMessages = async () => {
        try {
            const response = await fetch("https://message-api-withmongo-lzf4.onrender.com/api/v1/messages/");
            const data = await response.json();

            // Access the messages array in the data object and map over it to get the message
            allMessages.data = data.data[0].messages.map(item => item.message);
        } catch (error) {
            console.log(error);
        }
    };

    // function to sendMessage to the API
    const sendMessage = async () => {
        try {
            const response = await fetch("https://message-api-withmongo-lzf4.onrender.com/api/v1/messages/", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    message: message.value,
                }),
            });
            const data = await response.json();

            // Update the reactive variable directly
            allMessages.data.push(message.value);
            console.log(message.value);
            message.value = "";
        } catch (error) {
            console.log(error);
        }
    };

    onMounted(() => {
        fetchMessages();
    });
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
