<script setup>
import { reactive, ref } from 'vue';

// Note: 画像はどこに配置するのが適切か？
const imgUrl = '/mei-miteki.webp';
// const todos = [
//   'buy milk',
//   'go to gym',
//   'study javascript'
// ]
// const todos = reactive([
//   'buy milk',
//   'go to gym',
//   'study javascript'
// ]) 
const todos = reactive([
  {
    id: crypto.randomUUID(),
    title: 'Item 0'
  },
  {
    id: crypto.randomUUID(),
    title: 'Item 1'
  },
  {
    id: crypto.randomUUID(),
    title: 'Item 2'
  }
]) 

const newTodo = ref('newTodo');

function addTodo(e) {
  // Note: リロードしないように
  // e.preventDefault();
  // alert(newTodo.value);
  e.preventDefault();
  todos.push(
    {
      id: crypto.randomUUID(),
      title: newTodo.value
    }
  );
  newTodo.value = '';
}

function handleInput(e) {
  newTodo.value = e.target.value;
}
</script>

<template>
  <div class="container">
    <h1>Todos</h1>
    <ul>
      <li v-for="todo in todos" :key="todo.id">{{ todo.title }}</li>
    </ul>
    <form @submit="addTodo">
      <!-- <input type="text" :value="newTodo" @input="handleInput"> -->
      <input type="text" v-model="newTodo">
      
      <button>Add</button>
    </form>
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