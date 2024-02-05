<template>
  <main>
    <TheWelcome />
    <DataList :data="dataList" @item-click="handleItemClick" @add-item="addItem" />
  </main>
</template>

<script setup lang="ts">
import DataList from '@/components/DataList.vue';
import TheWelcome from '@/components/TheWelcome.vue';
import { ref } from 'vue';


const dataList = ref([
  { id: 1, name: 'Item 1', type: 'string' },
  { id: 2, name: 'Item 2', type: 'number' },
  { id: 3, name: 'Item 3', type: 'string' },
  { id: 4, name: 'Item 4', type: 'boolean' },
]);

const handleItemClick = (item: { id: number; name: string; type: string; backgroundColor?: string }) => {
  item.backgroundColor = '#FFFF00';
};

const addItem = (newItem: { name: string; type: string }) => {
  if (newItem && newItem.name && newItem.type) {
    dataList.value.push({ id: dataList.value.length + 1, ...newItem });
  } else {
    console.error('Error: El nuevo ítem no es válido.');
  }
};
</script>

<style scoped></style>