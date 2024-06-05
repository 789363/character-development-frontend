<template>
  <div id="app">
    <h1>Character Development System</h1>
    <div>
      <input v-model="newUsername" placeholder="Enter username">
      <button @click="createUser">Create User</button>
    </div>
    <h2>Users</h2>
    <ul>
      <li v-for="user in users" :key="user.id">
        {{ user.username }} - Exp: {{ user.experience }}, Gold: {{ user.gold }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      users: [],
      newUsername: ''
    };
  },
  methods: {
    async createUser() {
      const response = await axios.post('http://localhost:3000/users', {
        username: this.newUsername
      });
      this.users.push(response.data);
      this.newUsername = '';
    },
    async fetchUsers() {
      const response = await axios.get('http://localhost:3000/users');
      this.users = response.data;
    }
  },
  mounted() {
    this.fetchUsers();
  }
};
</script>
