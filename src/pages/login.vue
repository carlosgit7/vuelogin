<script setup>
    import { useRouter } from "vue-router";
    import { useForm, useField } from 'vee-validate';
    import * as yup from 'yup';

    const schema = yup.object({
      username: yup.string().required().email().label("Email"),
      password: yup.string().required().min(8).label("Password"),
    });

    useForm({
      validationSchema: schema,
    });

    const { value: username, errorMessage: emailError } = useField('username');
    const { value: password, errorMessage: passwordError } = useField('password');


    import userAuth from "../composables/userAuth";
    import loginError from "../composables/loginError";
    


    const {isAuthenticated, login, signup, googleLogin} = userAuth();

    //const username = ref("");
    //const password = ref("");

    const router = useRouter();

    const logginIn = async() => {
        await login(username.value, password.value);
        goToHome();
 };

    const signingUp = async () => {
        await signup(username.value, password.value);
        goToHome();
 };

    const google = async() => {
      await googleLogin();
      goToHome();
    };

    const goToHome = () => {
        if (isAuthenticated.value) {
            router.push("/");
        } else {
            setError("Invalid username or password");
            start();
        }
 };

    const { error, setError } = loginError()

    import { useTimeout, promiseTimeout } from "@vueuse/core";

    const { ready, start } = useTimeout(3000, { controls: true });

</script>

<template>
<div class="flex flex-col items-center justify-center min-h-screen-nonav space-y-5">
  <h1 class="text-6xl tracking-tighter font-light">Login</h1>
  <div class="shadow-2xl border-1 rounded-md flex items-center justify-center bg-slate-300 overflow-hidden">
  <img src="../assets/loginBG.png" alt="bg-image" class="h-48">
  <form @submit.prevent="logginIn" class="flex flex-col space-y-1 p-3">
      <input type="text" name="username" placeholder="Email" v-model="username"
      :class="!ready && error ? 'border-2 border-red-500 p-1 rounded-md' : 'p-1 rounded-md'"
      />
      <span class="text-xs text-center text-red-600">{{emailError}}</span>
      <input type="password" name="password" placeholder="Password" v-model="password"
      :class="!ready && error ? 'border-2 border-red-500 p-1 rounded-md' : 'p-1 rounded-md'"
      />
      <span class="text-xs text-center text-red-600">{{passwordError}}</span>
      <!-- <button type="submit" @submit.prevent="logginIn" class="bg-cyan-700 text-black py-1 rounded-md">Login</button> -->
      <div class="flex space-x-1 text-black">
          <button
            type="submit"
            @submit.prevent="logginIn"
            class="w-1/2 py-1 bg-rose-600 rounded-md hover:bg-rose-700 mb-2"
          >
            Login
          </button>
          <button
            @click="signingUp"
            class="w-1/2 py-1  bg-blue-600 rounded-md hover:bg-blue-700 mb-2"
          >
            Sing Up
          </button>
        </div>
          <button
            @click="google"
            class="bg-green-400 hover:bg-green-500 rounded-md"
          >
            <img src="https://upload.wikimedia.org/wikipedia/commons/2/2f/Google_2015_logo.svg" class="m-auto object-cover h-8 w-auto" alt="Google_2015_logo">
          </button>
  </form>
  </div>
  <div v-if="!ready && error" class="absolute w-1/3 px-4 py-3 text-center text-red-800 bg-red-300 rounded-lg bottom-2 right-2 shadow-inner">
      {{ error }}
  </div>
</div>
</template>