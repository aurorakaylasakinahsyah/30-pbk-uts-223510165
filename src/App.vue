<template>
  <div>
    <header class="header">
      <nav class="menu">
        <ul>
          <li><router-link to="/">Home</router-link></li>
          <li><router-link to="/todos">Todos</router-link></li>
          <li><router-link to="/posts">Posts</router-link></li>
          <li><router-link to="/albums">Albums</router-link></li>
          <li><router-link to="/about">About</router-link></li>
        </ul>
      </nav>
    </header>
    <router-view></router-view>
  </div>
</template>

<style>
.header {
  background-color: #ffc0cb; /* Pink background */
  padding: 20px;
  text-align: center;
  border-bottom: 5px solid #ff69b4; /* Bright pink border */
}

.menu ul {
  display: flex;
  justify-content: center;
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu ul li {
  margin: 0 15px;
}

.menu ul li a {
  text-decoration: none;
  color: #ffffff; 
  font-weight: bold;
  font-size: 30px; 
  padding: 10px 20px; 
  border-radius: 20px; 
  transition: background-color 0.3s, transform 0.3s; 
  background-color: #ff69b4; /* Pink background */
}

.menu ul li a:hover {
  background-color: #ffb6c1; /* Lighter pink on hover */
  transform: scale(1.1); /* Slightly larger on hover */
}
</style>
