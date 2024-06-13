<script setup>
import { ref, onMounted, watch } from 'vue';

const selectedUser = ref(null);
const users = ref([]);
const posts = ref([]);
const selectedUserName = ref('');

const fetchUsers = async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    users.value = await response.json();
  } catch (error) {
    console.error('Error fetching users:', error);
  }
};

const fetchPosts = async () => {
  if (!selectedUser.value) return;
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser.value}`);
    posts.value = await response.json();
    selectedUserName.value = users.value.find(user => user.id === selectedUser.value)?.name || '';
  } catch (error) {
    console.error('Error fetching posts:', error);
  }
};

onMounted(fetchUsers);

watch(selectedUser, fetchPosts);
</script>

<template>
  <section class="post-section">
    <h2>Postingan Pengguna</h2>
    <div class="select-user">
      <label>Pilih Pengguna:</label>
      <select v-model="selectedUser" class="select-box">
        <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
      </select>
    </div>
    <div v-if="posts.length > 0" class="user-posts">
      <h3>Postingan Pengguna: {{ selectedUserName }}</h3>
      <table class="post-table">
        <thead>
          <tr>
            <th>Judul</th>
            <th>Isi</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="post in posts" :key="post.id">
            <td>{{ post.title }}</td>
            <td>{{ post.body }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>
  <img src="https://images.unsplash.com/photo-1532089006060-d3a39e2175f3?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwzNzE3NnwwfDF8c2VhcmNofDV8fHBsYXlmdWx8ZW58MHx8fHwxNjU3NzY1MzM0&ixlib=rb-1.2.1&q=80&w=1080" alt="Background Image">
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Comic+Neue:wght@700&display=swap');

body {
  margin: 0;
  font-family: 'Comic Neue', cursive;
  background-color: #ffe4e1;
  color: #333;
}

.post-section {
  margin-top: 20px;
  text-align: center;
  position: relative;
  z-index: 1;
}

.select-user {
  margin-bottom: 20px;
}

.select-box {
  padding: 8px 12px;
  font-size: 16px;
  border: 2px solid #ff69b4;
  border-radius: 5px;
  background-color: #ffcccb;
  transition: border-color 0.3s, background-color 0.3s;
}

.select-box:focus {
  outline: none;
  border-color: #ff1493;
  background-color: #ffebef;
}

.user-posts {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  margin: 0 auto;
  max-width: 800px;
}

.post-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.post-table th,
.post-table td {
  padding: 12px;
  border: 1px solid #ddd;
}

.post-table th {
  background-color: #ffb6c1;
}

.post-table td {
  background-color: white;
}

.post-table tr:hover {
  background-color: #ffcccb;
}

img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -1; 
}

h2, h3, label {
  color: #ff1493;
  text-shadow: 1px 1px #ff69b4;
}
</style>
