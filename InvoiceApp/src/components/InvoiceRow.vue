<script setup>
const emit = defineEmits(['add', 'remove'])
</script>

<template>
  <tr>
    <td>
      <button type="button" @click="emit('add')">+</button>
      <button type="button" @click="emit('remove')">-</button>
    </td>
    <td><input type="text" placeholder="Description" /></td>
    <td><input type="number" min="0" value="1" /></td>
    <td><input type="number" min="0" step="0.01" value="0.00" /></td>
    <td class="subtotal">$0.00</td>
  </tr>
</template>