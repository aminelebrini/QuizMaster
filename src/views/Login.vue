<template>
  <div class="relative min-h-screen overflow-hidden bg-gradient-to-br from-indigo-50 via-white to-cyan-50 flex items-center justify-center px-4 py-12">
    <div class="pointer-events-none absolute inset-0 bg-[linear-gradient(120deg,rgba(99,102,241,0.10)_0%,rgba(255,255,255,0)_35%,rgba(6,182,212,0.10)_100%)]"></div>

    <div class="relative w-full max-w-md">
      <div class="bg-white rounded-2xl shadow-2xl ring-1 ring-slate-200 overflow-hidden">
        <div class="bg-gradient-to-r from-indigo-500 to-purple-600 px-8 py-6">
          <h1 class="text-3xl font-bold text-white text-center mb-6">QuizMaster</h1>
          <p class="text-white text-center text-sm">Login to your account</p>
        </div>

        <div class="p-8">
          <form class="space-y-5" @submit.prevent="login">
            <div>
              <label class="block text-sm font-semibold text-gray-700 mb-2">Email Address</label>
              <input
                v-model="email"
                type="email"
                placeholder="you@example.com"
                required
                class="w-full px-4 py-2.5 border-2 border-gray-200 rounded-lg focus:border-indigo-500 focus:outline-none transition-colors"
              />
            </div>

            <div>
              <label class="block text-sm font-semibold text-gray-700 mb-2">Password</label>
              <input
                v-model="password"
                type="password"
                placeholder="••••••••"
                required
                class="w-full px-4 py-2.5 border-2 border-gray-200 rounded-lg focus:border-indigo-500 focus:outline-none transition-colors"
              />
            </div>

            <label class="flex items-center gap-2 text-gray-700 cursor-pointer">
              <input
                v-model="rememberMe"
                type="checkbox"
                class="w-4 h-4 rounded text-indigo-500 cursor-pointer"
              />
              <span class="text-sm">Remember me</span>
            </label>

            <button
              type="submit"
              class="w-full bg-gradient-to-r from-indigo-500 to-purple-600 text-white font-bold py-2.5 rounded-lg hover:from-indigo-600 hover:to-purple-700 transition-all duration-300 shadow-lg hover:shadow-xl"
            >
              Sign In
            </button>

            <p class="text-center text-sm">
              <a href="#" class="text-indigo-600 hover:text-indigo-700 font-medium">Forgot password?</a>
            </p>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import router from '@/router'
import { ref } from 'vue'

interface User {
  fullname: string
  email: string
  password: string
}

const email = ref<string>('')
const password = ref<string>('')
const rememberMe = ref<boolean>(false)

const user: User = {
  fullname: 'AMINE LEBRINI',
  email: 'aminelb@gmail.com',
  password: '123',
}

const login = (): void => {
  if (email.value === user.email && password.value === user.password) {
    localStorage.setItem('user', JSON.stringify(user))
    router.push({ name: 'home' })
    return
  }

  alert('Invalid email or password.')
}
</script>
