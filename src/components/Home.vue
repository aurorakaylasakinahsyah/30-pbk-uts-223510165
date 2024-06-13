<template>
    <div class="home-container">
      <div class="home-content">
        <h1 class="home-title">LEBIH DEKAT DENGAN AURORA</h1>
        <p class="home-description">Temukan Keunikan Aurora</p>
        <router-link to="/about" class="btn" @click="handleAboutClick">Tentang Aurora</router-link>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      handleAboutClick() {
        this.$router.push('/about');
      }
    }
  }
  </script>
  
  <style scoped>
  .home-container {
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
  
  .home-content {
    text-align: center;
    background: rgba(255, 192, 203, 0.8);
    padding: 30px;
    border-radius: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    animation: fadeIn 2s ease-in-out;
  }
  
  .home-title {
    font-size: 40px;
    font-weight: bold;
    color: #ff69b4;
    margin-bottom: 20px;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
    animation: slideIn 1s ease-out;
    font-family: 'Comic Sans MS', cursive, sans-serif;
  }
  
  .home-description {
    font-size: 20px;
    color: #fff;
    margin-bottom: 30px;
    animation: fadeInUp 1.5s ease-in-out;
    font-family: 'Comic Sans MS', cursive, sans-serif;
  }
  
  .btn {
    padding: 10px 20px;
    background-color: #ff69b4;
    color: #fff;
    text-decoration: none;
    border-radius: 20px;
    transition: background-color 0.3s, transform 0.3s;
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
    font-family: 'Comic Sans MS', cursive, sans-serif;
  }
  
  .btn:hover {
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
  