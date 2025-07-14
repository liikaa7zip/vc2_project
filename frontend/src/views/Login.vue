<template>
  <section class="bg-gradient-to-br  via-purple-100 to-pink-100 min-h-screen flex items-center justify-center px-6 py-12">
    <div class="w-full max-w-md bg-white dark:bg-gray-900 rounded-3xl shadow-2xl p-8">
      <h2 class="text-3xl font-extrabold text-center text-gray-900 dark:text-white mb-2">
        Welcome back 👋
      </h2>
      <p class="text-center text-sm text-gray-500 dark:text-gray-400 mb-6">
        Sign in to access your dashboard
      </p>

      <form @submit.prevent="login" class="space-y-5">
        <div>
          <label for="email" class="block mb-1 text-sm font-medium text-gray-900 dark:text-white">Email address</label>
          <input v-model="email" type="email" id="email" placeholder="you@example.com"
            class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 bg-gray-50 dark:bg-gray-800 dark:border-gray-600 dark:text-white" required />
        </div>

        <div>
          <label for="password" class="block mb-1 text-sm font-medium text-gray-900 dark:text-white">Password</label>
          <input v-model="password" type="password" id="password" placeholder="••••••••"
            class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 bg-gray-50 dark:bg-gray-800 dark:border-gray-600 dark:text-white" required />
        </div>

        <div class="flex items-center justify-between text-sm">
          <label class="flex items-center space-x-2">
            <input type="checkbox" class="form-checkbox text-blue-600 rounded border-gray-300 dark:border-gray-600" />
            <span class="text-gray-700 dark:text-gray-300">Remember me</span>
          </label>
          <a href="#" class="text-blue-600 hover:underline dark:text-blue-400">Forgot password?</a>
        </div>

        <button type="submit"
          class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold rounded-lg py-2 transition duration-200">
          Sign in
        </button>

        <p class="text-sm text-center text-gray-600 dark:text-gray-400 mt-4">
          Don't have an account?
          <a href="/register" class="text-blue-600 dark:text-blue-400 font-medium hover:underline">Sign up</a>
        </p>

        <p v-if="message" class="text-center mt-4 text-sm font-medium text-red-600 dark:text-red-400">
          {{ message }}
        </p>
      </form>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const email = ref('')
const password = ref('')
const message = ref('')

const login = async () => {
  try {
    const res = await axios.post('http://localhost:5000/api/auth/login', {
      email: email.value,
      password: password.value
    })
    message.value = 'Login successful!'
    localStorage.setItem('token', res.data.token)
    // Optional: redirect or emit event
  } catch (err) {
    message.value = err.response?.data?.message || 'Login failed'
  }
}
</script>
