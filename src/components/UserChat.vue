<template>
  <div class="chat-container">
    <h2>Chat</h2>
    <input v-model="recipientId" placeholder="Recipient ID"/>
    <button @click="findUser">Найти</button>
    <div v-if="userFound" class="chat-window">
      <h3>Chat with {{ recipientId }}</h3>
      <div v-for="(msg, index) in messages" :key="index" class="message">
        <p><strong>{{ msg.senderId }}:</strong> {{ msg.message }}</p>
      </div>
      <input v-model="message" placeholder="Message"/>
      <button @click="sendMessage">Отправить</button>
    </div>
  </div>
</template>

<script>
import io from 'socket.io-client';
export default {
  name: 'UserChat',
  data() {
    return {
      socket: null,
      recipientId: '',
      message: '',
      messages: [],
      userFound: false,
    };
  },
  props: ['userId'],
  mounted() {
    this.socket = io('http://localhost:3000');
    this.socket.emit('register', this.userId);
    this.socket.on('receive_message', (data) => {
      this.messages.push(data);
    });
  },
  methods: {
    findUser() {
      this.userFound = true;
    },
    sendMessage() {
      this.socket.emit('send_message', {
        senderId: this.userId,
        recipientId: this.recipientId,
        message: this.message,
      });
      this.messages.push({ message: this.message, senderId: this.userId });
      this.message = '';
    },
  },
};
</script>

<style scoped>


</style>