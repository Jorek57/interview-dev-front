<script setup>
import axios from 'axios'
import { ref } from 'vue'

let user = {
    username: '',
    password: ''
}

async function register() {
    try {
      const response = await axios.post('http://localhost:8000/api/register', user)
      console.log(response.data)
    } catch (error) {
        console.error('Error:', error)
    }

}
</script>

<template>
  <h1>Login</h1>
  <DsfrInput
    class="fr-mb-7v fr-my-7v"
    v-model="user.username"
    label="Username"
    type="text"
    :labelVisible="true"
    :required="true"
    placeholder="Johnny93"
  />
  <DsfrInput
    class="fr-mb-7v fr-my-7v"
    v-model="user.password"
    label="Password"
    type="password"
    :labelVisible="true"
    :required="true"
    placeholder="********"
  />
  <DsfrButton
    class="fr-mb-7v"
    label="Register"
    @click="register"
    :disabled="true"
  />
</template>
