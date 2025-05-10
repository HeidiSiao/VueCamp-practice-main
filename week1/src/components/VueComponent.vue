<template>
  <div class="flex-col">
    <label for="name">商品名稱</label>
    <input class="space-s" type="text" v-model="newName" id="name" />
    <label for="account">商品數量</label>
    <input class="space-s" type="number" v-model="newNumber" id="account" />
    <button class="space-s" type="button" @click="addProduct">增加</button>
  </div>
  <div class="space-s">
    {{ items }}
  </div>
  <table>
    <thead>
      <tr>
        <th>標題</th>
        <th>數量</th>
        <th>調整數量</th>
        <th>刪除</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in items" :key="item.id">
        <td>{{ item.name }}</td>
        <td>{{ item.account }}</td>
        <td><input type="number" v-model="item.account" /></td>
        <td>
          <button type="button" @click="deleteItem(item.id)">刪除品項</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
import { ref } from "vue";

const newName = ref("");
const newNumber = ref(0);

const items = ref([
  {
    id: 1,
    name: "蜂蜜鬆餅",
    account: 42,
  },
  {
    id: 2,
    name: "草莓大福",
    account: 7,
  },
  {
    id: 3,
    name: "珍珠奶茶",
    account: 89,
  },
  {
    id: 4,
    name: "芋泥球",
    account: 15,
  },
  {
    id: 5,
    name: "抹茶蛋糕",
    account: 63,
  },
]);

const addProduct = () => {
  items.value.push({
    id: new Date().getTime(),
    name: newName.value,
    account: newNumber.value,
  });
  newName.value = "";
  newNumber.value = 0;
};

const deleteItem = (targetId) => {
  // 防呆:避免在找不到對應項目時誤刪錯誤資料index是-1的value
  //   if (index !== -1) {
  //   items.value.splice(index, 1);
  // }
  items.value = items.value.filter((item) => item.id !== targetId);
};
</script>

<style scoped>
.space {
  margin: 50px;
}

.space-s {
  margin: 8px;
}

table,
td {
  border-collapse: separate;
  border-spacing: 20px 10px;
  border: 1px solid tan;
  border-radius: 5px;
  padding: 4px;
  text-align: center;
}

.flex-col {
  display: flex;
  flex-direction: column;
  align-items: start;
}
</style>
