<script setup lang="ts"></script>

<template>
  <div class="app">
    <div class="game-image">
      <img :src="currentImage" alt="Current Room" />
    </div>

    <div class="text-description">
      <p>{{ description }}</p>
    </div>

    <div class="inventory">
      <div v-for="(item, index) in inventory" :key="index" class="inventory-item">
        <img :src="item.icon" :alt="item.name" />
      </div>
    </div>

    <div class="actions">
      <button v-for="action in actions" :key="action" @click="performAction(action)">
        {{ action }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const currentImage = ref('/images/start-room.png');
const description = ref('You are standing in a dimly lit room. There is a door to the north.');
const inventory = ref([
  { name: 'Key', icon: '/icons/key.png' },
  { name: 'Note', icon: '/icons/note.png' }
]);
const actions = ['Look', 'Take', 'Use', 'Talk'];

function performAction(action) {
  // Replace with real game logic
  description.value = `You chose to: ${action}`;
}
</script>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  overflow: hidden;
  font-family: sans-serif;
}

.game-image {
  flex: 2;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #222;
}

.game-image img {
  max-height: 100%;
  max-width: 100%;
}

.text-description {
  flex: 1;
  padding: 1rem;
  background-color: #f0f0f0;
  font-size: 1rem;
  overflow-y: auto;
}

.inventory {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0.5rem;
  background: #ddd;
  overflow-x: auto;
}

.inventory-item {
  width: 48px;
  height: 48px;
  margin: 0 6px;
}

.inventory-item img {
  width: 100%;
  height: auto;
}

.actions {
  display: flex;
  justify-content: space-around;
  padding: 0.5rem;
  background: #ccc;
}

.actions button {
  flex: 1;
  margin: 0 4px;
  padding: 0.75rem;
  font-size: 1rem;
}
</style>