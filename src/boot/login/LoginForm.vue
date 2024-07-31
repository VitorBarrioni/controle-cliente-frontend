<template>
  <div class="login-container">
    <div class="login-box">
        <q-input label="E-mail" v-model="email"/>
        <q-input label="Senha" type="password" v-model="password"/>
        <q-btn type="positive" label="Login" @click="entrar"/>
      </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { api } from 'boot/axios'
import { useRouter } from 'vue-router'

const router = useRouter()

const email = ref('')
const password = ref('')

const entrar = async () => {
  const res = await api.post('/auth/login', {
    email: email.value,
    password: password.value
  })
  localStorage.setItem('token', res.data.token)
  router.push('/')
}

</script>

<style>

.login-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: linear-gradient(135deg, #6b7c93, #f2f2f2);
    margin: 0;
}

.login-box {
    background: white;
    padding: 2rem;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    width: 300px;
    text-align: center;
}

.q-input, .q-btn {
    margin-bottom: 1rem;
}
</style>
