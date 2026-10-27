<script setup>
import { ref, computed } from 'vue'
import InvoiceRow from '../components/InvoiceRow.vue'

let nextId = 1
const makeRow = () => ({ id: nextId++, description: '', qty: 1, price: 0 })

// The list of rows this page owns
const rows = ref([makeRow(), makeRow(), makeRow()])

const fmt = new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' })

// Insert a blank row after the clicked row
function addRow(index) {
  rows.value.splice(index + 1, 0, makeRow())
}

// Remove the clicked row, but always keep at least one
function removeRow(index) {
  if (rows.value.length > 1) {
    rows.value.splice(index, 1)
  }
}

// Invoice total: add up quantity x price for every row
const total = computed(() => {
  return rows.value.reduce((sum, r) => {
    return sum + (Number(r.qty) || 0) * (Number(r.price) || 0)
  }, 0)
})
</script>

<template>
  <main class="invoice">
    <h1>Invoice</h1>

    <table>
      <thead>
        <tr>
          <th>Add Or Remove Row</th>
          <th>Item Name</th>
          <th>Quantity</th>
          <th>Unit Price</th>
          <th>Subtotal</th>
        </tr>
      </thead>

      <tbody>
        <InvoiceRow
          v-for="(row, index) in rows"
          :key="row.id"
          v-model="rows[index]"
          @add="addRow(index)"
          @remove="removeRow(index)"
        />
      </tbody>

      <tfoot>
        <tr>
          <td colspan="4" class="label">Total</td>
          <td class="total">{{ fmt.format(total) }}</td>
        </tr>
      </tfoot>
    </table>
  </main>
</template>

<style scoped>
table { border-collapse: collapse; width: 100%; }
th, td { border: 1px solid #ccc; padding: 0.5rem; text-align: left; }
td.label, td.total { text-align: right; font-weight: bold; }
</style>