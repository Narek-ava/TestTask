<template>
  <div>
    <form @submit.prevent="addUser">
      <input v-model="newUser.name" placeholder="Name" required />
      <button type="submit">Add User</button>
    </form>
    <ul>
      <li v-for="user in users" :key="user.id">
        {{ user.name }} - {{ user.description }}
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
      newUser: { name: '' },
      nameError: null,
    };
  },
  methods: {
    fetchUsers() {
      axios.get('http://localhost:8000/api/users').then(response => {
        this.users = response.data;
      });

    },
    addUser() {
      axios.post('http://localhost:8000/api/users', this.newUser).then(() => {
        this.fetchUsers();
        this.newUser.name = '';
      });
    },
  },
  mounted() {
    this.fetchUsers();
  },

};
</script>
