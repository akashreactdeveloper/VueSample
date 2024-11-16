<script setup lang="ts">
import { ref } from 'vue'

// Example dynamic content, such as user login state
const isLoggedIn = ref(false)
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="logo">
      Akash
        <img src="" alt="Logo">
      </div>
      <nav class="nav-menu">
        <ul>
          <li><a href="#home">Home</a></li>
          <li><a href="#about">About</a></li>
          <li><a href="#services">Services</a></li>
          <li><a href="#contact">Contact</a></li>
        </ul>
      </nav>
      <div class="cta">
        <button v-if="!isLoggedIn">Sign Up</button>
        <button v-if="isLoggedIn">Log Out</button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

.logo img {
  height: 50px;
}

.nav-menu ul {
  list-style: none;
  display: flex;
  gap: 1.5rem;
  margin: 0;
  padding: 0;
}

.nav-menu a {
  text-decoration: none;
  color: #333;
  font-weight: bold;
}

.nav-menu a:hover {
  color: #007BFF;
}

.cta button {
  padding: 0.5rem 1rem;
  border: none;
  background-color: #007BFF;
  color: #fff;
  font-weight: bold;
  border-radius: 4px;
  cursor: pointer;
}

.cta button:hover {
  background-color: #0056b3;
}
</style>
