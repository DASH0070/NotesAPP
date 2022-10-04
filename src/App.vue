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

// USERS DATA
const database = ref<{ userName: string, password: string }[]>([]);

// NOTES DATA
let notesData = ref<{ [userName: string]: string[] }[]>([]);

const handleSignUpResponse = (msg: string) => {
    notesData.value.push({ [msg[0]]: [] });
    notesData.value.sort((a, b) => a.userName > b.userName ? 1 : -1);
}
let user = ref('');
let userIndex = ref();
const handleSignInResponse = (msg: string) => {
    for (let i = 0; i < notesData.value.length; i++) {
        if (notesData.value[i].hasOwnProperty(msg[0])) {
            user.value = msg[0];
            userIndex.value = i;
        }
    }
    router.value.activeLink = routerValues.notes;
}

</script>

<template>

    <SignIn key="2" @submit="(msg) => handleSignInResponse(msg as unknown as string)" :database="database"
        :router="router" v-if="router.activeLink === routerValues.signIn" />
    <SignUp key="1" @submit="(msg) => handleSignUpResponse(msg as unknown as string)" :database="database"
        :router="router" v-if="router.activeLink === routerValues.signUp" />
    <Notes :router="router" :notesData="notesData[userIndex][user]" v-if="router.activeLink === routerValues.notes" />
</template>

