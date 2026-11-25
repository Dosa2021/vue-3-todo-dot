<script setup>

const props = defineProps({
    todos: Array
})
const emit = defineEmits(['checkTodoEvent']);

function handleCheck(todo) {
    // console.log(todo.isCompleted);
    emit('checkTodoEvent', todo);
}

</script>

<template>
    <ul>
        <li v-for="todo in todos" :key="todo.id">
            <label>
                <input 
                    type="checkbox" 
                    :checked="todo.isCompleted"
                    @click="handleCheck(todo)"
                >
                {{ todo.title }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
    ul {
        margin: 0;
        padding: 0;
        list-style: none;
    }
    label:has(:checked) {
        color: #ddd;
        text-decoration: line-through;
    }
</style>