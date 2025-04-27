<script setup>
import { ref } from 'vue'
const text = ref('嗨')

const todos = ref([
  {
    id: 1745774181702,
    item: '吃蛋糕',
  },
  {
    id: 2735784651709,
    item: '吃炸雞',
  },
])

// 新增暫存空物件 -->為了編輯用
const tempEdit = ref ({
  id: '',
  text: ''
})


// 新增待辦
const addTodo = () => {
  todos.value.push({
    id: new Date().getTime(),
    item: text.value,
  })
  text.value = ''
}

// 刪除待辦
const deleteTodo =(todo) => {
  // const index = todos.value.findIndex(item => item.id === todo.id);
  // console.log(index);
  // todos.value.splice(index,1);
  todos.value = todos.value.filter( item => item.id !== todo.id)
}

// 編輯待辦
const setEditItem = (todo) => {
  // tempEdit.value = todo;
  // 物件傳參考原會直接連動修改->淺拷貝
  tempEdit.value = {...todo};
}

const enterEdit = () => {
   const index = todos.value.findIndex(item => item.id === tempEdit.value.id);
   todos.value[index] = tempEdit.value
}
</script>

<template>
  <div class="container">

    <section class="flex">
      <h3 class="area-title">待辦事項啦</h3>
      <input type="text" v-model="text" />
      <button type="button" @click="addTodo">Add Item</button>
    </section>


  <section class="todo-section">
  <!-- 
    <div class="todo-box" v-for="[key, value] in Object.entries(todos)" :key="key">
    <p>{{ key }} : {{ value }}</p>
  </div> -->
    <div class="todo-box" v-for="todo in todos" :key="todo.id">
      <div v-for="[key, value] in Object.entries(todo)" :key="key">
      <p>{{ key }}: {{ value }}</p>
    </div>
    <div class="flex">
      <button @click="deleteTodo(todo)">Delete</button>
      <button @click="setEditItem(todo)">Edit</button>
    </div>
    </div>
  </section>

  <section class="flex">
    <h3 class="area-title">編輯區域啦</h3>
    <input type="text" v-model="tempEdit.item">
    <button type="button" @click="enterEdit">Enter</button>
  </section>
</div>
</template>

<style scoped>
.todo-section {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  align-items: center;
  justify-content: center;
  margin-block: 8px;
  padding: 4px;
}

.todo-box {
  display: flex;
  padding-inline: 6px;

  border-style: inset;
  border-width: 12px;
  border-image: url('../assets/blossom2.jpg') 8% stretch;
  flex-direction: column;
  gap: 4px;

  color: slategrey;
  font-weight: bold;
  background-color: aliceblue;
}



.area-title {
  font-weight: 700;
  text-align: center;
  margin-block: 8px;
  margin-inline: 8px;
}

.container {
  width: 50%;
  margin: 24px auto;
  background-color: lightgoldenrodyellow;
}

.flex {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  
}

button {
  border-radius: 6px;
  color: whitesmoke;
  background-color: cadetblue;
  padding: 6px;
  margin: 4px;
  font-weight: bold;
}

input {
  margin-inline: 8px;

}
</style>
