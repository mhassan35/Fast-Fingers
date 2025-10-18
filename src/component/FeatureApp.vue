<template>
    <div class="top-panel">
      <ul class="panel-list">
        <li
          v-for="(item, index) in panelItems"
          :key="index"
          :class="{ active: item.active, divider: item.divider }">
          <i v-if="item.icon && !item.divider" :class="item.icon"></i>
          <span v-if="item.label && !item.divider">{{ item.label }}</span>
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const panelItems = ref([
  { label: 'punctuation', icon: 'fa-solid fa-at', active: false },
  { label: 'numbers', icon: 'fa-solid fa-hashtag', active: false },
  { divider: true }, // first divider after first two items
  { label: 'time', icon: 'fa-regular fa-clock', active: true },
  { label: 'words', icon: 'fa-solid fa-font', active: false },
  { label: 'quote', icon: 'fa-solid fa-quote-left', active: false },
  { label: 'zen', icon: 'fa-solid fa-triangle-exclamation', active: false },
  { label: 'custom', icon: 'fa-solid fa-wrench', active: false },
  { label: '15', icon: null, active: false },
  { label: '30', icon: null, active: false },
  { label: '60', icon: null, active: false },
  { label: '120', icon: null, active: false },
  { divider: true }, // second divider before timer
  { label: '', icon: 'fa-solid fa-xmark', active: false }
])
  </script>

  <style scoped>
  .top-panel {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #2C2E31;
    margin: 1rem 6rem 1rem 6rem;
    padding: 10px;
    border-radius: 18px;
    color: rgba(255, 255, 255, 0.5);
    font-size: 0.9rem;
  }
  
  .panel-list {
    list-style: none;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1.8rem;
    padding: 0;
    margin: 0;
    flex-wrap: wrap;
  }
  
  .panel-list li {
    display: flex;
    align-items: center;
    gap: 2px;
    cursor: pointer;
    opacity: 0.6;
    transition: color 0.3s ease, opacity 0.3s ease;
  }
  .panel-list li.divider {
    width: 2px;
    background-color: rgba(255, 255, 255, 0.3);
    height: 30px;
    margin: 0 10px;
    pointer-events: none;
  }
  .panel-list li:hover {
    opacity: 1;
    color: #FFD43B;
  }
  
  .panel-list .active {
    color: #FFD43B;
    opacity: 1;
  }
</style>
  