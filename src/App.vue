<script setup>
import PostList from './components/PostList.vue'
</script>

<template>
  <header>
    <h1>Consumo de API - Vue 3</h1>
  </header>

  <main>
    <PostList />
  </main>
</template>

<style>
/* Reset básico para tirar margens do navegador */
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #fff;
}

#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  color: #333;
}

header {
  text-align: center;
  margin-bottom: 40px;
  border-bottom: 2px solid #42b983;
  padding-bottom: 10px;
}
</style>