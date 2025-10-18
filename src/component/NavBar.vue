<template>
    <div class="navbar">
      <span class="logo">Fast Typing ...</span>
      <nav>
        <ul>
          <li><i class="fa-regular fa-keyboard"></i></li>
          <li><i class="fa-solid fa-circle-info"></i></li>
          <li @click="showPopup = true">
            <i class="fa-solid fa-circle-user"></i>
          </li>
        </ul>
      </nav>
  
      <!-- Auth Popup -->
      <AuthPopup v-model="showPopup" />
    </div>
  </template>
  
  <script setup>
  import { ref } from "vue";
  import AuthPopup from "./AuthPopup.vue";
  
  const showPopup = ref(false);
  </script>
  
  <style scoped>
  .navbar {
    padding: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 24px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.5);
  }
  .logo {
    color: green;
  }
  nav ul {
    display: flex;
    list-style: none;
    gap: 1rem;
  }
  nav li {
    cursor: pointer;
    opacity: 0.4;
    border-radius: 20px;
    padding: 2px;
    color: white;
  }
  nav li:hover {
    opacity: 0.7;
  }
  nav i {
    font-size: 24px;
  }
  </style>
  