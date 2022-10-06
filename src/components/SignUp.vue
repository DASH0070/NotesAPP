<script setup lang="ts">

import { ref } from 'vue';

const props = defineProps<{ router: { activeLink: string } }>();    // RECIEVE ROUTER AS POPS
const { router } = props;
const userData = ref<{ userName: string, password: string }>({ userName: '', password: '' });  // STORE USERNAME, PASSWORD ENTER IN FIELD

// HANDLE FORM SUBMIT
const handleSignUp = () => {
    if (!userData.value.userName || !userData.value.password) {
        alert('Enter All Fields');
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