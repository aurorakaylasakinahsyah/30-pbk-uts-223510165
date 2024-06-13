<template>
    <div class="album-container">
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
              <img :src="photo.thumbnailUrl" @click="showPhoto(photo.url)" class="photo-thumbnail">
            </td>
            <td>{{ photo.title }}</td>
          </tr>
        </tbody>
      </table>
      <div v-else class="no-photos">
        <p>Tidak ada foto yang tersedia.</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  import { useRoute } from 'vue-router'
  
  const route = useRoute()
  const selectedAlbum = ref(route.params.id)
  const albums = ref([])
  const photos = ref([])
  const backgroundUrl = ref('url(\'https://i.pinimg.com/originals/7b/55/b4/7b55b4f2f9453b99b0f8a1e896f6d795.jpg\')')
  
  const fetchAlbums = async () => {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/albums')
      albums.value = await response.json()
    } catch (error) {
      console.error('Error fetching albums:', error)
    }
  }
  
  const fetchPhotos = async () => {
    try {
      const response = await fetch(`https://jsonplaceholder.typicode.com/albums/${selectedAlbum.value}/photos`)
      photos.value = await response.json()
    } catch (error) {
      console.error('Error fetching photos:', error)
    }
  }
  
  const showPhoto = (url) => {
    window.open(url, '_blank')
  }
  
  onMounted(() => {
    fetchAlbums()
    fetchPhotos()
  })
  </script>
  
  <style scoped>
  .album-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    background-color: #ffe4e1;
    border-radius: 15px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    animation: fadeIn 2s ease-in-out;
  }
  
  .title {
    font-size: 24px;
    color: #ff69b4;
    margin-bottom: 15px;
    font-family: 'Comic Sans MS', cursive, sans-serif;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
    animation: slideIn 1s ease-out;
  }
  
  .album-select {
    padding: 10px;
    font-size: 16px;
    border: 2px solid #ff69b4;
    border-radius: 10px;
    background-color: #fff;
    color: #ff69b4;
    margin-bottom: 20px;
    cursor: pointer;
    transition: border-color 0.3s;
  }
  
  .album-select:hover {
    border-color: #ff1493;
  }
  
  .photos-table {
    width: 100%;
    max-width: 800px;
    border-collapse: collapse;
  }
  
  .photos-table th,
  .photos-table td {
    padding: 10px;
    border: 1px solid #ff69b4;
    text-align: center;
  }
  
  .photo-thumbnail {
    width: 100px;
    height: 100px;
    object-fit: cover;
    border: 2px solid #ff69b4;
    border-radius: 10px;
    cursor: pointer;
    transition: transform 0.3s, border-color 0.3s;
  }
  
  .photo-thumbnail:hover {
    transform: scale(1.1);
    border-color: #ff1493;
  }
  
  .no-photos {
    text-align: center;
    margin-top: 20px;
    color: #ff69b4;
  }
  
  @keyframes fadeIn {
    0% { opacity: 0; }
    100% { opacity: 1; }
  }
  
  @keyframes slideIn {
    0% { transform: translateY(-20px); opacity: 0; }
    100% { transform: translateY(0); opacity: 1; }
  }
  </style>
  