<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import { useQuery } from '@tanstack/vue-query'

const { isPending, isFetching, isError, data, error } = useQuery({
  queryKey: ['todos'],
  queryFn: async () => {
    const response = await fetch('http://localhost:8000/todos')
    return response.json()
  }
})
</script>

<template>

  <div>
    <HelloWorld />
    <div v-if="isPending">Loading...</div>
    <div v-if="isError">{{ error }}</div>
    <div v-if="isFetching">Refetching...</div>
    <div v-if="data">
      <ul>
        <li v-for="todo in data">{{ todo.title }}</li>
      </ul>
    </div>
  </div>
  
</template>
