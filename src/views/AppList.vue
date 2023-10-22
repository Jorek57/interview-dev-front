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
let hashDatas = ref([]); // Initialize as an empty array

async function getHash() {
  try {
    const response = await axios.post('http://localhost:8000/api/hash', toHash);

    // Create a new object to represent the hash data
    const newHashData = {
      title: "The hash for the string " + toHash.string + " with the algorithm " + toHash.algorithm + " is:",
      description: response.data.hash
    };

    // Push the new hash data object to the hashDatas array
    hashDatas.value.unshift(newHashData);

    console.log(hashDatas.value);
  } catch (error) {
    console.error('Error:', error);
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
