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


const dataList = ref( [
  { id: 1, name: 'Machu Picchu', type: 'Historical Site' },
  { id: 2, name: 'Grand Canyon', type: 'Natural Wonder' },
  { id: 3, name: 'Eiffel Tower', type: 'Landmark' },
  { id: 4, name: 'Great Barrier Reef', type: 'Natural Wonder' },
  { id: 5, name: 'Pyramids of Giza', type: 'Historical Site' },
  { id: 6, name: 'Taj Mahal', type: 'Architectural Marvel' },
  { id: 7, name: 'Venice Canals', type: 'Scenic Waterways' },
  { id: 8, name: 'Banff National Park', type: 'National Park' },
  { id: 9, name: 'Santorini', type: 'Island Paradise' },
  { id: 10, name: 'Yellowstone National Park', type: 'National Park' },
]);

const handleItemClick = (item: { id: number; name: string; type: string; backgroundColor?: string }) => {
  item.backgroundColor = '#2ecc71';
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