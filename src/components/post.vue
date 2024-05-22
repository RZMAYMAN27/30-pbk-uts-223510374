<template>
  <div class="profile">
    <h1>POST</h1>
    <div>
      <label for="users">Pilih User:</label>
      <select id="users" v-model="selectedUserId" @change="loadUserPosts">
        <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
      </select>
    </div>
    <div>
      <label for="color">Pilih Warna Teks:</label>
      <select id="color" v-model="selectedColor">
        <option v-for="color in colors" :key="color.value" :value="color.value">{{ color.name }}</option>
      </select>
    </div>
    <div class="user-posts">
      <div v-if="loading">Loading...</div>
      <div v-else>
        <div v-for="post in userPosts" :key="post.id">
          <h2 :style="{ color: selectedColor }">{{ post.title }}</h2>
          <p :style="{ color: selectedColor }">{{ post.body }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [],
      selectedUserId: null,
      userPosts: [],
      loading: false,
      colors: [
        { name: 'Merah', value: 'red' },
        { name: 'Hijau', value: 'green' },
        { name: 'Biru', value: 'blue' },
        { name: 'Kuning', value: 'yellow' },
        { name: 'Ungu', value: 'purple' },
        { name: 'Hitam', value: 'black' },
        { name: 'Putih', value: 'white' }
      ],
      selectedColor: 'black'
    };
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(data => {
          this.users = data;
        })
        .catch(error => {
          console.error('Error fetching users:', error);
        });
    },
    loadUserPosts() {
      if (!this.selectedUserId) return;
      this.loading = true;
      fetch(`https://jsonplaceholder.typicode.com/posts?userId=${this.selectedUserId}`)
        .then(response => response.json())
        .then(data => {
          this.userPosts = data;
          this.loading = false;
        })
        .catch(error => {
          console.error('Error fetching user posts:', error);
          this.loading = false;
        });
    }
  }
};
</script>

<style>
.profile {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.profile h1 {
  font-family: 'Segoe UI', 'Tahoma', 'Geneva', 'Verdana', sans-serif;
  color: #100e0f;
  text-align: center;
}

.user-posts {
  margin-top: 20px;
}

.user-posts h2, .user-posts p {
  font-family: 'Segoe UI', 'Tahoma', 'Geneva', 'Verdana', sans-serif;
}
</style>
