<script setup lang="ts">
import { ref } from 'vue'

const props = defineProps<{ notesData: string[], router: { activeLink: string } }>();   // Recieve All Notes data of User as Props
let { notesData, router } = props;

// Add Notes button
const addNotes = () => {
    notesData.push('');
}

// remove Notes Button
const removeNotes = (index: number) => {
    for (let i = index; i < notesData.length - 1; i++) {
        notesData[i] = notesData[i + 1];
    }
    notesData.pop();
}

</script>
<template>

    <div class="flex flex-wrap gap-10">
        <div v-for="(elem, index) in notesData">
            <textarea v-model="notesData[index]" :key="index" class="w-60 h-40 border-2 ">{{elem}}</textarea>
            <button @click="removeNotes(index)">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="w-6 h-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                </svg>
            </button>
        </div>
    </div>
    <button @click="addNotes" class="my-10 bg-slate-700 text-slate-50 rounded-full w-28 h-8 block mx-auto">Add
        Notes</button>
    <button @click="router.activeLink = 'signIn'"
        class="my-0 bg-slate-700 text-slate-50 rounded-full w-28 h-8">Back</button>

</template>