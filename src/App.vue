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
const handleSignInResponse = (msg: string, notes: string) => {
    user.value = msg;
    router.value.activeLink = routerValues.notes;
}

</script>

<template>

    <SignIn key="2" @signup="router.activeLink = routerValues.signUp" @submit="(msg, notes) => handleSignInResponse(msg as unknown as string, notes)"
        v-if="router.activeLink === routerValues.signIn" />
    <SignUp key="1" @signin="router.activeLink = routerValues.signIn" v-if="router.activeLink === routerValues.signUp" />
    <Notes @signin="router.activeLink = routerValues.signIn" :user="user" v-if="router.activeLink === routerValues.notes" />
</template>

