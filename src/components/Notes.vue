<script setup lang="ts">
import { ref, watch } from 'vue'

const props = defineProps<{ user: string}>();   // Recieve All Notes data of User as Props
let { user } = props;
const emit = defineEmits(['signin'])
let notesData = ref<[string, string[]]>(JSON.parse(localStorage.getItem(user) as string));
// Add Notes button
const addNotes = () => {
    notesData.value[1].push('');
}
console.log(notesData.value)

// remove Notes Button
const removeNotes = (index: number) => {
    for (let i = index; i < notesData.value[1].length - 1; i++) {
        notesData.value[1][i] = notesData.value[1][i + 1];
    }
    notesData.value[1].pop();
}
watch(notesData.value, (newKey) => localStorage.setItem(user, JSON.stringify(newKey)));

const selected = ref<boolean[]>([]);
for (let i = 0; i < notesData.value[1].length; i++) {
    selected.value?.push(false);
}
console.log(selected.value)

</script>
<template>

    <div class="flex flex-wrap justify-center gap-10 relative">
        <div v-for="(elem, index) in notesData[1]" class="w-60 h-40 "
            :class="selected[index] ? 'w-96 h-96 absolute left-1/2 top-1/2 -translate-x-1/2 ' : '' ">
            <textarea @focusout="selected[index] = false" @focus="selected[index] = true" v-model="notesData[1][index]"
                :key="index" class="w-full h-full outline-none">{{ elem }}</textarea>
            <button @click="removeNotes(index)" :class="selected[index] ? 'translate-x-44 -translate-y-96' : ''"
                class="translate-x-24 -translate-y-40">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="w-6 h-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                </svg>
            </button>
        </div>
    </div>
    <button @click="addNotes" class="my-10 bg-slate-700 text-slate-50 rounded-full w-28 h-8 block mx-auto">Add
        Notes</button>
    <button @click="emit('signin')"
        class="my-0 bg-slate-700 text-slate-50 rounded-full w-28 h-8">Back</button>

</template>