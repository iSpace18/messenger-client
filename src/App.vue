<template>
  <div id="app">
    <div v-if="!loggedIn">
      <UserLogin @login="handleLogin"/>
    </div>
    <div v-else>
      <UserChat :userId="userId"/>
    </div>
  </div>
</template>

<script>
import UserLogin from './components/UserLogin.vue';
import UserChat from './components/UserChat.vue';

export default {
  data() {
    return {
      loggedIn: false,
      userId: '',
    };
  },
  methods: {
    handleLogin(userId) {
      this.userId = userId;
      this.loggedIn = true;
    },
  },
  components: {
    UserLogin,
    UserChat,
  },
};
</script>
<style>
body{
  color: white;
  text-align: center;
  background-color: rgb(70, 114, 180);
}
h2{
background-color:black;
width: 175px;
margin: 0 auto;
padding: 5px;
margin-bottom: 30px;
}
input{
  padding: 5px;
  border-radius: 5px;
  border: none;
  background-color: black;
  color: white;
}
button{
  border: none;
  border-radius: 5px;
  padding: 5px;
  background-color: rgb(0, 0, 0);
  color: white;
  margin-left: 10px;
  padding-left: 15px;
  padding-right: 15px;
}
.chat-container {
  background-color: #0000008e;
  padding: 20px;
  border-radius: 10px;
}

.chat-window {
  background-color: #0000008e;
  padding: 15px;
  border-radius: 5px;
  margin-top: 20px;
}

.message {
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
}

</style>