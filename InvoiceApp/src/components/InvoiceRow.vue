<script setup>
import { computed } from 'vue';

const row = defineModel({ required: true })
const emit = defineEmits(['add', 'remove'])
const fmt = new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' })
// Row subtotal: quantity x unit price
const subtotal = computed(() => {
  return (Number(row.value.qty) || 0) * (Number(row.value.price) || 0)
})
</script>

<template>
  <tr>
    <td>
      <button type="button" @click="emit('add')">+</button>
      <button type="button" @click="emit('remove')">-</button>
    </td>
    <td><input type="text" placeholder="Description" v-model="row.description" /></td>
    <td><input type="number" min="0" value="1" v-model.number="row.qty" /></td>
    <td><input type="number" min="0" step="0.01" value="0.00" v-model.number="row.price" /></td>
    <td class="subtotal">{{ fmt.format(subtotal) }}</td>
  </tr>
</template>