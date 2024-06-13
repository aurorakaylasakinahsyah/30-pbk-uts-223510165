<template>
    <div class="album-details-container" :style="{ backgroundImage: backgroundUrl }">
      <h2 class="title">Pilih Album:</h2>
      <select v-model="selectedAlbum" @change="fetchPhotos" class="album-select">
        <option v-for="album in albums" :key="album.id" :value="album.id">{{ album.title }}</option>
      </select>
      <h2 class="title">Foto dalam Album {{ selectedAlbum }}</h2>
      <table v-if="photos.length" class="photos-table">
        <thead>
          <tr>
            <th>Thumbnail</th>
            <th>Judul</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="photo in photos" :key="photo.id" class="photo-row">
            <td>
              <img :src="photo.thumbnailUrl" @click="showPhoto(photo.url)" class="thumbnail">
            </td>
            <td>{{ photo.title }}</td>
          </tr>
        </tbody>
      </table>
      <div v-else class="no-photos">
        <p>Tidak ada foto tersedia.</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, watch } from 'vue'
  import { useRoute } from 'vue-router'
  
  const route = useRoute()
  const selectedAlbum = ref(route.params.id)
  const albums = ref([])
  const photos = ref([])
  const backgroundUrl = ref('url(\'https://th.bing.com/th/id/OIP.s3fJbDvDCIxPaR_Cq7K8VwHaHa?w=1024&h=1024&rs=1&pid=ImgDetMain\')')
  
  const fetchAlbums = async () => {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/albums')
      albums.value = await response.json()
    } catch (error) {
      console.error('Kesalahan saat mengambil album:', error)
    }
  }
  
  const fetchPhotos = async () => {
    try {
      const response = await fetch(`https://jsonplaceholder.typicode.com/albums/${selectedAlbum.value}/photos`)
      photos.value = await response.json()
    } catch (error) {
      console.error('Kesalahan saat mengambil foto:', error)
    }
  }
  
  const showPhoto = (url) => {
    window.open(url, '_blank')
  }
  
  onMounted(() => {
    fetchAlbums()
    fetchPhotos()
  })
  
  watch(selectedAlbum, () => {
    fetchPhotos()
  })
  </script>
  
  <style scoped>
  .album-details-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    background-size: cover;
    background-position: center;
    min-height: 100vh;
  }
  
  .title {
    color: #007bff;
    text-align: center;
  }
  
  .album-select {
    margin: 20px auto;
    display: block;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    outline: none;
  }
  
  .photos-table {
    margin: 20px auto;
    border-collapse: collapse;
  }
  
  .photos-table th,
  .photos-table td {
    border: 1px solid #007bff;
    padding: 10px;
    text-align: center;
  }
  
  .thumbnail {
    width: 100px;
    height: 100px;
    object-fit: cover;
    border: 1px solid #007bff;
    border-radius: 5px;
    cursor: pointer;
    transition: border-color 0.3s;
  }
  
  .thumbnail:hover {
    border-color: #0056b3;
  }
  
  .no-photos {
    text-align: center;
    margin-top: 20px;
  }
  </style>
  