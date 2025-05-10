<script setup>
import { ref } from "vue";
import VueComponent from "./components/VueComponent.vue";

// 把資料抽出來
// 由資料驅動畫面 響應式
const items = ref([
  {
    id: 1,
    name: "購買雜貨",
    dueDate: "2024-07-30",
    completed: true,
  },
  {
    id: 2,
    name: "完成報告",
    dueDate: "2024-08-01",
    completed: false,
  },
  {
    id: 3,
    name: "清理房間",
    dueDate: "2024-07-28",
    completed: true,
  },
  {
    id: 4,
    name: "計劃假期",
    dueDate: "2024-08-05",
    completed: false,
  },
  {
    id: 5,
    name: "處理稅務",
    dueDate: "2024-08-10",
    completed: false,
  },
]);
</script>

<template>
  <h2>Week-01</h2>
  <table>
    <thead>
      <tr>
        <th>代辦事項名稱</th>
        <th>到期日</th>
        <th>完成狀況</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item of items" :key="item.id">
        <td>{{ item.name }}</td>
        <td>{{ item.dueDate }}</td>
        <td>{{ item.completed ? "是" : "否" }}</td>
        <!-- 三元運算 -->
      </tr>
    </tbody>
  </table>
  <hr />
  <h2>Week-02</h2>
  <VueComponent />
</template>

<style scoped></style>
