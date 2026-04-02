<template>
    <header class="sticky top-0 z-50 bg-gradient-to-r from-indigo-500 to-purple-600 shadow-lg">
        <div class="max-w-6xl mx-auto px-4 md:px-8 py-4 flex flex-col md:flex-row justify-between items-center gap-4 md:gap-0">
            <h1 class="text-3xl md:text-4xl font-bold text-white tracking-tight hover:scale-105 transition-transform duration-300 cursor-pointer">
                QuizMaster
            </h1>
            <div class="w-full md:w-auto flex flex-col md:flex-row items-center gap-4 md:gap-6">
                <nav class="w-full md:w-auto">
                    <ul class="flex flex-wrap justify-center md:justify-end gap-4 md:gap-8 list-none p-0 m-0">
                    <li class="relative">
                        <a href="#" class="text-white font-medium text-sm md:text-base hover:text-yellow-300 hover:border-b-2 hover:border-yellow-300 transition-all duration-300 pb-1 inline-block hover:-translate-y-0.5">
                            Home
                        </a>
                    </li>
                    <li class="relative">
                        <a href="#" class="text-white font-medium text-sm md:text-base hover:text-yellow-300 hover:border-b-2 hover:border-yellow-300 transition-all duration-300 pb-1 inline-block hover:-translate-y-0.5">
                            Quiz
                        </a>
                    </li>
                    <li class="relative">
                        <a href="#" class="text-white font-medium text-sm md:text-base hover:text-yellow-300 hover:border-b-2 hover:border-yellow-300 transition-all duration-300 pb-1 inline-block hover:-translate-y-0.5">
                            About
                        </a>
                    </li>
                    <li class="relative">
                        <a href="#" class="text-white font-medium text-sm md:text-base hover:text-yellow-300 hover:border-b-2 hover:border-yellow-300 transition-all duration-300 pb-1 inline-block hover:-translate-y-0.5">
                            Contact
                        </a>
                    </li>
                    </ul>
                </nav>

                <div class="flex items-center gap-3 rounded-full bg-white/20 px-3 py-2 text-white backdrop-blur-sm">
                    <div class="h-9 w-9 rounded-full bg-white/30 flex items-center justify-center text-sm font-bold">
                        {{ loguedUser?.fullname.charAt(0) }}
                    </div>
                    <div class="text-xs leading-tight">
                        <p class="font-semibold">{{ loguedUser?.fullname }}</p>
                        <p class="opacity-90">{{ loguedUser?.email }}</p>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>

<script setup lang="ts">

interface User {
    fullname: string
    email: string
    password: string
}

const userData = localStorage.getItem('user');
const loguedUser: User | null = userData ? JSON.parse(userData) : null;

</script>