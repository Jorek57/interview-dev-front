<script setup>
import axios from 'axios'
import { ref } from 'vue'

const options = [
    {
        label: "MD5",
        value: "md5"
    },
    {
        label: "SHA1",
        value: "sha1"
    },
    {
        label: "SHA256",
        value: "sha256"
    },
    {
        label: "All of them",
        value: "all"
    }
]
const headers = [
    "String",
    "Algorithm",
    "Hash"
]
let toHash = {
    string: '',
    algorithm: ''
}
let hashDatas = ref([])

async function getHash() {
    try {
    if (toHash.algorithm === 'all') {
      for (const option of options) {
        if (option.value !== 'all') {
          const response = await axios.post('http://localhost:8000/api/hash', {
            string: toHash.string,
            algorithm: option.value,
          })

          const newHashData = {
            title: "The hash for the string " + toHash.string + " with the algorithm " + option.value + " is:",
            description: response.data.hash
          }

          hashDatas.value.unshift(newHashData)
        }
      }
    } else {
      const response = await axios.post('http://localhost:8000/api/hash', toHash)

      const newHashData = {
        title: "The hash for the string " + toHash.string + " with the algorithm " + toHash.algorithm + " is:",
        description: response.data.hash
      }
      hashDatas.value.unshift(newHashData)
    }
  } catch (error) {
    console.error('Error:', error)
  }

}
</script>

<template>
  <h1>Second exercise</h1>
  <DsfrInput
    class="fr-mb-7v fr-my-7v"
    v-model="toHash.string"
    label="Insert the string you want to hash"
    type="text"
    :labelVisible="true"
    :required="true"
    placeholder="qwertyuiop"
  />
  <DsfrRadioButtonSet
  class="fr-mb-7v fr-my-7v"
    legend="Choose the hash algorithm you want to use"
    v-model="toHash.algorithm"
    name="radio-set"
    :options="options"
    :inline="true"
    :required="true"
  />
  <DsfrButton
  class="fr-mb-7v"
    label="Generate the hash"
    @click="getHash"
  />
  <DsfrTiles :tiles="hashDatas" :horizontal="true" />
</template>
