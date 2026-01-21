<script setup>
import { ref, onMounted } from 'vue'
import PostItem from './PostItem.vue'

const posts = ref([])
const loading = ref(false)
const error = ref(null)

const fetchPosts = async () => {
  loading.value = true
  error.value = null
  
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts')
    if (!response.ok) throw new Error('Falha ao conectar na API')
    const data = await response.json()
    posts.value = data.slice(0, 10) 
  } catch (err) {
    error.value = 'Erro: ' + err.message
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchPosts()
})
</script>

<template>
  <div class="post-list-container">
    <div class="header-actions">
      <h2>Últimas Postagens</h2>
      <button @click="fetchPosts" :disabled="loading" class="btn-reload">
        {{ loading ? 'Atualizando...' : 'Recarregar' }}
      </button>
    </div>

    <div v-if="loading" class="status">Carregando dados...</div>
    <div v-else-if="error" class="status error">{{ error }}</div>
    
    <div v-else class="list">
      <PostItem v-for="post in posts" :key="post.id" :post="post" />
    </div>
  </div>
</template>

<style scoped>
.header-actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
.btn-reload {
  padding: 8px 16px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.btn-reload:disabled { background-color: #a0dca0; }
.status { text-align: center; padding: 20px; font-weight: bold; }
.error { color: red; }
</style>