<script setup lang="ts">

const props = defineProps<{ database: { userName: string, password: string }[], router: { activeLink: string } }>();
const { database, router } = props;

const userData: { userName: string, password: string } = { userName: '', password: '' };    // STORES NEW USER DATA
const handleSignUp = () => {    // HANDLE FORM SUBMIT
    if (database.filter((elem) => elem.userName === userData.userName).length != 0) return; // CHECKING IF USERNAME ALREADY EXIST IN DATABASE
    database.push(userData);     // PUSHING NEW USER DATA IN DATABASE
    // database.sort(database.)

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
        <!-- SIGN IN BUTTON  -->
        <button @click="" class="text-left hover:underline duration-200 hover:text-yellow-700">
            Already Have an account? Sign In
        </button>
    </form>
</template>
<style scoped>

</style>