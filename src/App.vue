<script setup lang="ts">

import { ref, reactive } from 'vue';
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
const router = reactive<{ activeLink: routerValues }>({ activeLink: routerValues.signIn });

// USERS DATA
const database = reactive<{ userName: string, password: string }[]>([]);
database.push({userName: 'a', password: 'a'})

// NOTES DATA
const notesData = reactive<{[userName: string]: string[]}[]>([]);
notesData.push({'a': ['ADADA', 'asdasd', 'wrwerwrw']});


</script>

<template>
    <SignIn :database="database" :router="router" v-if="router.activeLink === routerValues.signIn" />
    <SignUp :database="database" :router="router" v-if="router.activeLink === routerValues.signUp" />
    <Notes :notesData="notesData[0].a" />
</template>

<style scoped>
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}
</style>
