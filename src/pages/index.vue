<script setup>
import { useRouter } from "vue-router";
import useAuth from "../composables/userAuth";
const { isAuthenticated, user } = useAuth();
</script>

<template>
<div class="flex flex-col items-center justify-center min-h-screen-nonav">
  <div v-if="!isAuthenticated" class="">
     <h1  class="text-6xl tracking-tighter font-extralight">Welcome</h1>
     <h2 class=" tracking-tighter font-extralight text-blue-700 ml-5">Please <router-link to="/login">login</router-link> or <router-link to="/login">create account</router-link></h2>
  </div>
   <h1 v-else class="text-6xl tracking-tighter font-extralight">Welcome {{ user }}</h1>
  <img src="../assets/indexBG.png" alt="bg-image" class="w-2/3 ">
</div>
</template>