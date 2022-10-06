<script setup lang="ts">

import { ref } from 'vue';
// Components Import
import SignIn from './components/SignIn.vue';
import SignUp from './components/SignUp.vue';
import Notes from './components/Notes.vue';

// Router VALUES
enum routerValues {
    signIn = 'signIn',
    signUp = 'signUp',
    notes = 'notes'
};

// ROUTER
const router = ref<{ activeLink: routerValues }>({ activeLink: routerValues.signIn });

let user = ref('');
const handleSignInResponse = (msg: string) => {
    user.value = msg;
}

</script>

<template>

    <SignIn key="2" @submit="(msg) => handleSignInResponse(msg as unknown as string)"
        :router="router" v-if="router.activeLink === routerValues.signIn" />
    <SignUp key="1" :router="router" v-if="router.activeLink === routerValues.signUp" />
    <Notes :user="user" :router="router" v-if="router.activeLink === routerValues.notes" />
</template>

