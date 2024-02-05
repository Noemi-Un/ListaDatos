<template>
    <div>
      <h2>Lista de Datos</h2>
      <ul>
        <li v-for="item in data" :key="item.id">
          <span v-if="item.id % 2 !== 0">{{ item.name }}</span>
          <span v-else>Item no accesible</span>
          <button @click="handleItemClick(item)">Seleccionar</button>
        </li>
      </ul>

      <div>
        <h3>Agregar Nuevo Item</h3>
        <input v-model="newItemName" placeholder="Nombre" />
        <input v-model="newItemType" placeholder="Tipo" />
        <button @click="addItem">Agregar</button>
      </div>
    </div>
</template>

<script setup lang="ts">

  import { ref } from 'vue'
  const props = defineProps<{
    data: Array<{ id: number; name: string; type: string; backgroundColor?: string }>
  }>()

  const emits = defineEmits<{
    (e: 'add-item', newItem:{ id: number; name: string; type: string; backgroundColor?: string } ): any
    (e: 'item-click', item: { id: number; name: string; type: string; backgroundColor?: string }): any
  }>()

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

</style>