<script setup>
  import { ref } from 'vue';
  import axios from 'axios';

  const apiUrl = import.meta.env.VITE_API_URL;
  console.log(apiUrl)
  axios.defaults.withCredentials = true;
  axios.defaults.withXSRFToken = true;

  const user = ref(null);
    
  const form = ref({
    email: '',
    password: '',
  })

  
  async function login() {
    try {
      console.log(form.value);
      await axios.get(`${apiUrl}/sanctum/csrf-cookie`);
      await axios.post(`${apiUrl}/login`, {
        email: form.value.email,
        password: form.value.password
      });

      let { data } = await axios.get(`${apiUrl}/api/user`);
      console.log(data);
      user.value = data;
    } catch (error) {
      if (error.response) {
        // O servidor retornou uma resposta com um código de status diferente de 2xx
        console.error('Erro durante o login:', error.response.data);
      } else if (error.request) {
        // A solicitação foi feita, mas não houve resposta do servidor
        console.error('Erro de solicitação:', error.request);
      } else {
        // Ocorreu um erro ao configurar a solicitação
        console.error('Erro ao configurar a solicitação:', error.message);
      }
    }
  }

  async function logout() {
    await axios.post(`${apiUrl}/logout`);
    user.value = null; // Limpar os dados do usuário após o logout
  }
   
</script>
  

<template>

<div v-if="user">
  {{ user }}
</div>

<div class="flex h-screen items-center justify-center">
        <button v-if="user" @click="logout()" class="bg-red-500 text-white font-semibold py-2 px-10 w-full rounded">
            Logout
        </button>
      <form @submit.prevent="login()" class="w-1/4 mx-auto p-4">
        <h1 class="font-semibold mb-2 text-xl">
          Login
        </h1>
        <div class="mb-4">
          <label for="email" class="block mb-1 text-sm">Email</label>
          <input
            type="text"
            v-model="form.email"
            class="w-full border rounded px-3 py-2"
            required
          />
        </div>
        <div class="mb-4">
          <label for="password" class="block mb-1 text-sm">Password</label>
          <input
            type="password"
            v-model="form.password"
            class="w-full border rounded px-3 py-2"
            required
          />
        </div>
        <button
          type="submit"
          class="bg-blue-500 text-white font-semibold py-2 px-10 w-full rounded"
        >
          Login
        </button>
      </form>
    </div>
  </template>
  
  