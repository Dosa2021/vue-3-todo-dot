<script setup>
// Note: 画像はどこに配置するのが適切か？
const imgUrl = '/mei-miteki.webp';
const todos = [
  'buy milk',
  'go to gym',
  'study javascript'
]

function addTodo(e) {
  // Note: リロードしないように
  e.preventDefault();
  alert('ok!');
}
</script>

<template>
  <div class="container">
    <h1>Todos</h1>
    <ul>
      <li v-for="todo in todos">{{ todo }}</li>
    </ul>
    <form @submit="addTodo">
      <input type="text">
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