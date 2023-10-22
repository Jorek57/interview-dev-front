<script setup>
import axios from 'axios'
import { ref } from 'vue'

const title = ref()
const description = ref()
const errorOccurred = ref(false)

import { onMounted } from 'vue'

onMounted(async () => {
  try {
    const response = await axios.get('http://localhost:8000/api/dummy-hash')
    title.value = "Here's a SHA256 hash for the string " + response.data.random_string + " :"
    description.value = response.data.random_hash
    errorOccurred.value = false
  } catch (error) {
    errorOccurred.value = true
    console.error('Error:', error)
  }
})
</script>

<template>
  <h1>First exercise</h1>
  <DsfrTile
    v-if="!errorOccurred"
    :title="title"
    :description="description"
    :disabled="true"
  />
  <DsfrAlert
    v-if="errorOccurred"
    title="Error"
    description="An error occured. Please try again later"
    type="error"
    :small="small"
    :closeable="false"
  />
</template>
