<script setup>
import axios from 'axios'
import { ref } from 'vue'

const title = ref("Here's a hash for the string ");
const description = ref()

import { onMounted } from 'vue';

onMounted(async () => {
  try {
    const response = await axios.get('http://localhost:8000/api/dummy-hash')
    title.value += response.data.random_string
    description.value = response.data.random_hash
  } catch (error) {
    console.error('Error:', error);
  }
});
</script>

<template>
  <h1>First exercise</h1>
  <DsfrTile
    :title="title"
    :description="description"
    :disabled="true"
  />
</template>
