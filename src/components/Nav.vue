<script setup>
import { useRouter } from "vue-router";
import userAuth from "../composables/userAuth"

const { isAuthenticated, logout } = userAuth();

const router = useRouter();

const loggingOut = () => {
  logout();
  router.push("/");
};

</script>
<template>
<div class="bg-lime-600 px-6">
    <div class="conitainer mx-auto flex justify-between items-center">
        <router-link to="/"><h1 class="tracking-tighter py-6 text-4xl font-light text-black hover:cursor-pointer">
            <span class="font-semibold">Chat</span>AppWithFirebase 
        </h1></router-link>
        <nav>
            <ul class="flex space-x-4 text-black">
                <router-link to="/"><li class="py-8 px-4 hover:cursor-pointer hover:bg-lime-700 hover:text-gray-200">Home</li></router-link>
                <router-link to="/about"><li class="py-8 px-4 hover:cursor-pointer hover:bg-lime-700 hover:text-gray-200">About</li></router-link>
                <router-link v-if="!isAuthenticated" to="/login"><li class="py-8 px-4 hover:cursor-pointer hover:bg-lime-700 hover:text-gray-200">Login</li></router-link>
                <div v-else class="flex">
                    <router-link to="/secret"><li class="py-8 px-4 hover:cursor-pointer hover:bg-lime-700 hover:text-gray-200">Secret</li></router-link>
                    <router-link to="/chat"><li class="py-8 px-4 hover:cursor-pointer hover:bg-lime-700 hover:text-gray-200">Chat</li></router-link>
                    <button @click="loggingOut"><li class="py-8 px-4 hover:cursor-pointer hover:bg-lime-700 hover:text-gray-200">Logout</li></button>
                </div>
            </ul>
        </nav>
    </div>
</div>
</template>