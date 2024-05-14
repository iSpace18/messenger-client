<template>
  <div>
    <h2>Введите ваш ID</h2>
    <input v-model="userId" placeholder="User ID"/>
    <button @click="register">Войти</button>
  </div>
</template>

<script>
export default {
  name: 'UserLogin',
  data() {
    return {
      userId: '',
    };
  },
  methods: {
    register() {
      if (this.userId.trim()) {
        this.$emit('login', this.userId);
      } else {
        alert('Введите корректный ID');
      }
    },
  },
};
</script>