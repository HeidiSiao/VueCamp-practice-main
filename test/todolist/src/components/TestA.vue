<script setup>
import { ref } from "vue";
const text = ref('這裡使用了ref');
const addItems = () => {
  todos.value.push({
    id: new Date().getTime(),
    text: text.value
  })
  text.value="";
};

const todos =ref([
  {
    id: 123,
    text: '我是文字'
  }
]) ;

</script>

<template>
  <input type="text" v-model="text">
  <button type="button" @click="addItems">新增待辦</button>
  <div v-for="todo in todos" :key="todo.id">
{{ todo.text }}
  </div>
</template>