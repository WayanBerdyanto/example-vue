<template>
  <div>
    <h1>HOME</h1>
    <router-link to="/test">Take me to Test page</router-link>
    <button @click.prevent="getUsers">Fetch User Data</button>

    <div v-if="users.length > 0">
      <h2>Users:</h2>
      <table border="1">
        <thead>
          <th>Username</th>
          <th>Nama</th>
          <th>Prodi</th>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>
              {{ user.username }}
            </td>
            <td>
              {{ user.nama }}
            </td>
            <td>
              {{ user.prodi }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <p v-if="error">{{ error }}</p>
  </div>
</template>
  
  <script>
import axios from "axios";
import { ref } from "vue";

const users = ref([]);
const error = ref(null);

const getUsers = async () => {
  try {
    const response = await axios.get("/api/users");
    users.value = response.data;

    console.log(response.data);
  } catch (err) {
    error.value = "Failed to fetch user data: " + err.message;
  }
};
try {
  const response = await axios.get("/api/users");
  users.value = response.data;

  console.log(response.data);
} catch (err) {
  error.value = "Failed to fetch user data: " + err.message;
}

export default {
  setup() {
    return {
      users,
      error,
      getUsers,
    };
  },
};
</script>
  