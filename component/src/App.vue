<script setup>
  import { ref, computed } from 'vue'
  import H1 from '@/components/H1.vue'
  import H2 from '@/components/H2.vue'
  import H3 from '@/components/H3.vue'
  import H4 from '@/components/H4.vue'
  
  // 將所有的 component 放入陣列中
  const components = [H1, H2, H3, H4]
  // 當前的 component index
  const currentIndex = ref(0)

  // 根據 currentIndex 計算出目前要顯示的 component
  const currentComponent = computed(() => components[currentIndex.value])

  // 切換到下一個 component
  function nextComponent() {
    currentIndex.value = (currentIndex.value + 1) % components.length
  }
</script>

<template>
  <div>
    <!-- 按鈕用來切換 component -->
    <button @click="nextComponent">下一個組件</button>
    <!-- 使用動態 component -->
    <component :is="currentComponent"></component>
  </div>
</template>

<style scoped>
button {
  margin-bottom: 20px;
}
</style>