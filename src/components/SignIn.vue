<script setup lang="ts">

import { ref } from 'vue';

// RECIEVE DATABASE AND ROUTER AS POPS

const userData = ref<{ userName: string, password: string }>({ userName: '', password: '' });
const emit = defineEmits(['submit', 'signup']);

// FORM SUBMIT HANDLER
const handleSignIn = () => {
    for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) === userData.value.userName) {
            if (JSON.parse(localStorage.getItem(localStorage.key(i) as string) as string)[0] !== userData.value.password) break;
            emit('submit', localStorage.key(i) as string)
            return;
        }
    }

    alert('Enter Valid Authentications');
    userData.value.userName = '';
    userData.value.password = '';
    return;
}

// SIGN UP BUTTON HANDLER
const handleSignUp = () => {
    emit('signup')
}

</script>
<template>

    <h1 class="text-slate-700 text-4xl">SIGN IN</h1>
    <!-- SIGN IN FORM  -->
    <form @submit.prevent="handleSignIn" class="flex flex-col items-left justify-center gap-10 w-96 mx-auto">
        <!-- USERNAME FIELD  -->
        <input v-model="userData.userName" type="text" placeholder="Username"
            class="border-2 focus:border-slate-900 rounded-full px-2 mt-10 outline-none" />
        <!-- PASSWORD FIELD  -->
        <input v-model="userData.password" type="password" placeholder="Password"
            class="border-2 focus:border-slate-900 rounded-full px-2 outline-none" />
        <!-- FORM SUBMIT / SIGN IN BUTTON  -->
        <button type="submit" class="bg-slate-600 text-slate-50 w-20 border-2 ease-out
             border-slate-600 rounded-full duration-200 hover:bg-slate-50
             hover:text-slate-600">
            Sign In
        </button>
    </form>
    <!-- SIGN UP BUTTON  -->
    <button @click="handleSignUp" class="text-left hover:underline duration-200 hover:text-yellow-700 my-10">
        Don't Have an account? Sign Up
    </button>

</template>