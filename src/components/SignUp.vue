<script setup lang="ts">

import { ref } from 'vue';

const props = defineProps<{ router: { activeLink: string } }>();    // RECIEVE ROUTER AS POPS
const { router } = props;
const userData = ref<{ userName: string, password: string, email: string, mobile?: number }>({ userName: '', password: '', email: '' });  // STORE USERNAME, PASSWORD ENTER IN FIELD

// HANDLE FORM SUBMIT
const handleSignUp = () => {
    console.log(userData.value)
    if (!userData.value.userName) {
        alert('Enter username');
        return;
    }
    if (userData.value.mobile?.toString().length != 10) {
        alert('Enter valid Mobile number');
        return;
    }
    if (!/.com$/.test(userData.value.email)) {
        alert('enter valid email');
        return;
    }
    if (userData.value.password.length < 8) {
        alert('password should contain atleast 8 character');
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
        <input v-model="userData.userName" type="text" placeholder="Username"
            class="border-2 focus:border-slate-900 rounded-full px-2 mt-10 outline-none" />
        <!-- EMAIL FIELD  -->
        <input v-model="userData.email" type="email" placeholder="Email"
            class="border-2 focus:border-slate-900 rounded-full px-2 outline-none" />
        <!-- MOBILE NUMBER FIELD  -->
        <input v-model="userData.mobile" type="number" placeholder="Mobile Number"
            class="border-2 focus:border-slate-900 rounded-full px-2 outline-none" />
        <!-- PASSWORD FIELD  -->
        <input v-model="userData.password" type="password" placeholder="Password"
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