<template>
  <div id="app">
    <header>
      <h1>CapVenture Game Creator</h1>
      <p>Create MacVenture-style adventure games</p>
    </header>

    <main>
      <div class="creator-workspace">
        <p>Game creation tools will be implemented here.</p>
        <ul>
          <li>Scene Editor</li>
          <li>Hotspot Creation Tool</li>
          <li>Script Editor</li>
          <li>Asset Manager</li>
          <li>Game Preview</li>
        </ul>
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
// Game creator logic will be implemented here
</script>

<style scoped>
#app {
  min-height: 100vh;
  padding: 20px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

header {
  text-align: center;
  margin-bottom: 2rem;
}

h1 {
  color: #2c3e50;
  margin-bottom: 0.5rem;
}

.creator-workspace {
  max-width: 1200px;
  margin: 0 auto;
  background: #f8f9fa;
  border-radius: 8px;
  padding: 2rem;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  background: white;
  margin: 0.5rem 0;
  padding: 1rem;
  border-radius: 4px;
  border-left: 4px solid #3498db;
}
</style>