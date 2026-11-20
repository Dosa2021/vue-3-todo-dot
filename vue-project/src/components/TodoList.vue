<script setup>
const props = defineProps({
    todos: Array
})
</script>

<template>
    <ul>
        <li v-for="todo in todos" :key="todo.id">{{ todo.title }}</li>
    </ul>
</template>