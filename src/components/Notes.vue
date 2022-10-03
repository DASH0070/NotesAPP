<script setup lang="ts">
import { reactive } from 'vue'

const props = defineProps<{ notesData: string[] }>();
const { notesData } = props;
const newData = reactive<string[]>([]);
for (let i in notesData) {
    newData[i] = notesData[i];
}


let i = 0;

</script>
<template>
    <div class="flex flex-wrap gap-10">
        <textarea  v-for="(elem, index) in notesData" v-model="notesData[index]" :key="index"
            class="w-60 h-40 border-2 ">{{elem}}</textarea>
    </div>
</template>