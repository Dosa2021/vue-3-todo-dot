<script setup>
import { onMounted, reactive, ref, watch } from 'vue';
import TodoList from './components/TodoList.vue';
import TodoAddForm from './components/TodoAddForm.vue';

// Note: 画像はどこに配置するのが適切か？
const imgUrl = '/mei-miteki.webp';
// const todos = reactive([
//   {
//     id: crypto.randomUUID(),
//     title: 'Item 0',
//     isCompleted: false
//   },
//   {
//     id: crypto.randomUUID(),
//     title: 'Item 1',
//     isCompleted: true
//   },
//   {
//     id: crypto.randomUUID(),
//     title: 'Item 2',
//     isCompleted: false
//   }
// ]) 
const todos = reactive([]);
const newTodo = ref('newTodo');

// function addTodo(e) {
//   // Note: リロードしないように
//   // e.preventDefault();
//   // alert(newTodo.value);
//   e.preventDefault();
//   if (newTodo.value.trim() === '') {
//     return
//   }

//   todos.push(
//     {
//       id: crypto.randomUUID(),
//       title: newTodo.value
//     }
//   );
//   newTodo.value = '';
// }

function addTodo(newTodo) {
  todos.push({
    id: crypto.randomUUID(),
    title: newTodo,
    isCompleted: false
  })
}

function toggleIsCompleted(todo) {
    const index = todos.findIndex((element) => {
      return element.id === todo.id;
    })
    todos[index].isCompleted = !todos[index].isCompleted;
}

function deleteTodo(todo) {
  if (confirm('Sure?') === false) {
    return;
  }

  const index = todos.findIndex((element) => {
    return element.id === todo.id;
  })
  todos.splice(index, 1)
}

function handleInput(e) {
  newTodo.value = e.target.value;
}

onMounted(() => {
  const savedTodos = localStorage.getItem('todos');
  if (savedTodos !== null) {
    const pasedTodos = JSON.parse(savedTodos);
    pasedTodos.forEach(element => {
      todos.push(element)
    });
  }
});

watch(
  todos,
  (updatedTodos) => {
    localStorage.setItem('todos', JSON.stringify(updatedTodos))
  }
)
</script>

<template>
  <div class="container">
    <h1>Todos</h1>
    <!-- <ul>
      <li v-for="todo in todos" :key="todo.id">{{ todo.title }}</li>
    </ul> -->
    <TodoList 
      :todos="todos" 
      @checkTodoEvent="toggleIsCompleted"
      @deleteTodoEvent="deleteTodo"
    />

    <!-- <form @submit="addTodo">
      <input type="text" v-model="newTodo">
      <button>Add</button>
    </form> -->
    <TodoAddForm @addTodoEvent="addTodo" />
  </div>

  <div class="img-mei">
    <img :src="imgUrl" alt="永野芽郁">
  </div>
</template>

<style scoped>
.container {
  width: 700px;
  margin: 0 auto;
  text-align: center;
  background-color: skyblue;
}
.container img {
  width: 50%;
}

h1 {
  font-size: 20px;
}

.img-mei {
  text-align: center;
  background-color: skyblue;
}
.img-mei img {
  width: 100%;
}

</style>