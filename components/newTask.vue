<script setup lang="ts">
import { nanoid } from "nanoid";
import type { Task } from "~~/types";

const emit = defineEmits<{
    (
        e: "add", payload: Task
    ): void
}>();

const focused = ref(false)
const title = ref("")


const createTask = (e: Event) => {
    if (title.value.trim()) {
        e.preventDefault();
        emit("add", {
            title: title.value.trim(),
            createdAt: new Date(),
            id: nanoid()
        } as Task)
    }

    title.value = ""
}
</script>

<template>
    <textarea v-model="title" @keydown.tab="createTask" @keyup.tab="createTask" class="{
        'h-7': !focused,
        'h-20' focused
      }" style="outline: none !important" @focus="focused = true" @blur="focused = false"
        :placeholder="!focused ? '+ Add a Card' : 'Enter a title for thir card'" />
</template>

