<script setup lang="ts">

import { ref } from 'vue';

const props = defineProps<{ router: { activeLink: string } }>();    // RECIEVE ROUTER AS POPS
const { router } = props;
const userData = ref<{ userName: string, password: string }>({ userName: '', password: '' });  // STORE USERNAME, PASSWORD ENTER IN FIELD

// HANDLE FORM SUBMIT
const handleSignUp = () => {
    if (userData.value.userName.length < 4) {
        alert('username should be atleast 4 characters long');
        return;
    }
    if (userData.value.password.length < 8) {
        alert('password should be atleast 8 characters long');
        return;
    }
    if (!/[0-9]/.test(userData.value.password)) {
        alert('password should contain atleast 1 numeric character');
        return;
    }
    if (!/[a-z]/.test(userData.value.password)) {
        alert('password should contain atleast 1 small case alphabet');
        return;
    }
    if (!/[A-Z]/.test(userData.value.password)) {
        alert('password should contain atleast 1 capital alphabet');
        return;
    }
    if (!/[^0-9a-zA-Z]/.test(userData.value.password)) {
        alert('password should contain atleast 1 special character');
        return;
    }
    // CHECKING IF USERNAME ALREADY EXIST IN DATABASE
    if (localStorage.getItem(userData.value.userName)) {
        alert('Username Already Exist');
        userData.value.userName = '';
        userData.value.password = '';
        return;
    }
    localStorage.setItem(userData.value.userName, JSON.stringify([userData.value.password, []]));
    router.activeLink = 'signIn';   // SETTING ROUTER TO SIGNIN
}

// HANDLE SIGN IN BUTTON LINK
const handleSignIn = () => {
    router.activeLink = 'signIn';   // SETTING ROUTER TO SIGN IN
}

</script>
<template>

    <h1 class="text-slate-700 text-4xl">SIGN UP</h1>
    <!-- SIGN UP FORM  -->
    <form @submit.prevent="handleSignUp" class="flex flex-col items-left justify-center gap-10 w-96 mx-auto">
        <!-- USERNAME FIELD  -->
        <input v-model="userData.userName" type="text" placeholder="Enter Username"
            class="border-2 focus:border-slate-900 rounded-full px-2 mt-10 outline-none" />
        <!-- PASSWORD FIELD  -->
        <input v-model="userData.password" type="password" placeholder="Enter Password"
            class="border-2 focus:border-slate-900 rounded-full px-2 outline-none" />
        <!-- FORM SUBMIT / SIGN UP BUTTON  -->
        <button type="submit" class="bg-slate-600 text-slate-50 w-20 border-2 ease-out
         border-slate-600 rounded-full duration-200 hover:bg-slate-50
         hover:text-slate-600">
            Sign Up
        </button>
    </form>
    <!-- SIGN IN BUTTON  -->
    <button @click="handleSignIn" class="text-left hover:underline duration-200 hover:text-yellow-700 my-10">
        Already Have an account? Sign In
    </button>

</template>