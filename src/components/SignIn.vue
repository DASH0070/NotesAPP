<script setup lang="ts">
const props = defineProps<{ database: { userName: string, password: string }[], router: { activeLink: string } }>();
const { database, router } = props;

const userData: { userName: string, password: string } = ({ userName: '', password: '' });

const handleSignIn = () => {    // FORM SUBMIT HANDLER
    // if (database.filter((elem) => elem.userName === userData.userName).length === 0) {    // CHECKING IF USERNAME ALREADY EXIST IN DATABASE
    //     alert('Enter Valid Authentications');
    //     return;
    // }
    router.activeLink = 'notes'
}

const handleSignUp = () => {    // SIGN UP BUTTON HANDLER
    router.activeLink = 'signUp';
}
</script>
<template>
    <h1 class="text-slate-700 text-4xl">SIGN IN</h1>
    <!-- SIGN IN FORM  -->
    <form @submit.prevent="handleSignIn" class="flex flex-col items-left justify-center gap-10 w-96 mx-auto">
        <!-- USERNAME FIELD  -->
        <input v-model="userData.userName" type="text" placeholder="Enter Username"
            class="border-2 focus:border-slate-900 rounded-full px-2 mt-10 outline-none" />
        <!-- PASSWORD FIELD  -->
        <input v-model="userData.password" type="password" placeholder="Enter Password"
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