<template>
    <div class="about-container">
      <div class="about-content">
        <h1 class="about-title">Tentang Aurora</h1>
        <p class="about-description">Saya adalah mahasiswi Universitas Islam Riau dengan program studi Teknik Informatika. Sekarang saya berada di semester 4 dan pada semester ini saya mempelajari mata kuliah Pemrograman Berbasis Komponen.</p>
        <button class="home-button" @click="goHome">Kembali ke Beranda</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      goHome() {
        this.$router.push('/');
      }
    }
  }
  </script>
  
  <style scoped>
  .about-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #ffccf9;
    background-image: url('https://i.pinimg.com/originals/7b/55/b4/7b55b4f2f9453b99b0f8a1e896f6d795.jpg');
    background-size: cover;
    background-position: center;
    padding: 20px;
  }
  
  .about-content {
    text-align: center;
    background: rgba(255, 192, 203, 0.8);
    padding: 30px;
    border-radius: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    animation: fadeIn 2s ease-in-out;
  }
  
  .about-title {
    font-size: 40px;
    font-weight: bold;
    color: #ff69b4;
    margin-bottom: 20px;
    animation: slideIn 1s ease-out;
    font-family: 'Comic Sans MS', cursive, sans-serif;
  }
  
  .about-description {
    font-size: 20px;
    color: #fff;
    margin-bottom: 30px;
    animation: fadeInUp 1.5s ease-in-out;
    font-family: 'Comic Sans MS', cursive, sans-serif;
  }
  
  .home-button {
    padding: 10px 20px;
    font-size: 18px;
    color: #fff;
    background-color: #ff69b4;
    border: none;
    border-radius: 20px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.3s;
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
    font-family: 'Comic Sans MS', cursive, sans-serif;
  }
  
  .home-button:hover {
    background-color: #ff1493;
    transform: scale(1.1);
  }
  
  @keyframes fadeIn {
    0% { opacity: 0; }
    100% { opacity: 1; }
  }
  
  @keyframes slideIn {
    0% { transform: translateY(-20px); opacity: 0; }
    100% { transform: translateY(0); opacity: 1; }
  }
  
  @keyframes fadeInUp {
    0% { transform: translateY(20px); opacity: 0; }
    100% { transform: translateY(0); opacity: 1; }
  }
  </style>
  