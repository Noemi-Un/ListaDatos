<template>
  <div class="data-list-container">
    <h2>Lista de Datos</h2>
    <ul class="data-list">
      <li :style="{outline : `${item.backgroundColor} 2px solid`} " v-for="item in data" :key="item.id" class="data-item" :class="{ 'odd-item': item.id % 2 !== 0 }">
        <span v-if="item.id % 2 !== 0">{{ item.name }}</span>
        <span v-else>Item no accesible</span>
        <button @click="handleItemClick(item)" class="select-button">Seleccionar</button>
      </li>
    </ul>

    <div class="add-item-container">
      <h3>Agregar Nuevo Item</h3>
      <div class="input-container">
        <input v-model="newItemName" placeholder="Nombre" class="input-field" />
        <input v-model="newItemType" placeholder="Tipo" class="input-field" />
      </div>
      <button @click="addItem" class="add-button">Agregar</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const props = defineProps<{
  data: Array<{ id: number; name: string; type: string; backgroundColor?: string }>;
}>();

const emits = defineEmits<{
  (e: 'add-item', newItem: { id: number; name: string; type: string; backgroundColor?: string }): any;
  (e: 'item-click', item: { id: number; name: string; type: string; backgroundColor?: string }): any;
}>();

const newItemName = ref('');
const newItemType = ref('');

const handleItemClick = (item: { id: number; name: string; type: string; backgroundColor?: string }) => {
  if (!item.backgroundColor) {
    emits('item-click', item);
  }
};

const addItem = () => {
  const newItem = { id: props.data.length + 1, name: newItemName.value, type: newItemType.value };
  emits('add-item', newItem);
  newItemName.value = '';
  newItemType.value = '';
};
</script>

<style scoped>
.data-list-container {
  max-width: 600px;
  margin: 0 auto;
}

.data-list {
  list-style-type: none;
  padding: 0;
}

.data-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  margin-bottom: 8px;
  background-color: #fff;
  border-radius: 8px;
  color: #2f2f2f;
}

.odd-item {
  background-color: #e0e0e0;
}

.select-button {
  background-color: #3498db;
  color: #fff;
  border: none;
  padding: 6px 12px;
  border-radius: 4px;
  cursor: pointer;
}

.add-item-container {
  margin-top: 20px;
}

.input-container {
  display: flex;
  gap: 10px;
}

.input-field {
  width: 150px;
  padding: 8px;
}

.add-button {
  background-color: #2ecc71;
  color: #fff;
  border: none;
  padding: 10px;
  border-radius: 4px;
  cursor: pointer;
}
</style>