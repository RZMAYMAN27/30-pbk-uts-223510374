<template>
  <div id="app">
    <h1>Daftar Barang</h1>
    <input type="text" v-model="newActivity.name" placeholder="Tambahkan barang baru">
    <div class="datetime-container">
      <label for="datetime">Tanggal & Jam:</label>
      <input id="datetime" type="datetime-local" v-model="newActivity.dateTime">
    </div>
    <button @click="addActivity">Tambah</button>
    <table>
      <thead>
        <tr>
          <th>Barang</th>
          <th>Tanggal & Jam</th>
          <th>Status</th>
          <th>Aksi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(activity, index) in activities" :key="index">
          <td>{{ activity.name }}</td>
          <td>{{ formatDate(activity.dateTime) }}</td>
          <td>
            <input type="checkbox" v-model="activity.completed">
            <span :class="{ 'completed': activity.completed }">{{ activity.completed ? 'Selesai' : 'Belum Selesai' }}</span>
          </td>
          <td><button @click="removeActivity(index)">Hapus</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: {
        name: '',
        dateTime: '',
        completed: false
      },
      activities: []
    };
  },
  methods: {
    addActivity() {
      if (this.newActivity.name && this.newActivity.dateTime) {
        this.activities.push({...this.newActivity});
        this.newActivity.name = '';
        this.newActivity.dateTime = '';
        this.newActivity.completed = false;
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    },
    formatDate(dateTime) {
      if (!dateTime) return '';
      const options = { year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit' };
      return new Date(dateTime).toLocaleDateString(undefined, options);
    }
  }
};
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>
