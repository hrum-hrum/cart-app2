<script setup>
import BasketTableItem from './BasketTableItem.vue'
import BasketTableSummary from './BasketTableSummary.vue'

defineProps({
  basket: {
    type: Array,
    required: true,
  },
  totalPrice: {
    type: Number,
    default: 0,
  },
})
</script>

<template>
  <table class="basket-table">
    <thead class="basket-table__header">
      <tr>
        <th>Product Details</th>
        <th>Price</th>
        <th>Quantity</th>
        <th>Subtotal</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody class="basket-table__body">
      <tr v-for="(item, index) in basket" :key="`product_${item.id}`">
        <BasketTableItem
          v-bind="item"
          @increase-item-quantity="$emit('increase-item-quantity', item)"
          @decrease-item-quantity="$emit('decrease-item-quantity', item)"
          @remove-item="$emit('remove-item', index)"
        />
      </tr>

      <tr v-if="!basket.length">
        <td colspan="5">
          <p class="basket-table__empty">No items</p>
        </td>
      </tr>

      <tr v-if="basket.length">
        <BasketTableSummary :total-price="totalPrice" />
      </tr>
    </tbody>
  </table>
</template>

<style>
.basket-table {
  width: 100%;
  border-collapse: collapse;
}

.basket-table__header {
  background-color: #3c4242;
  color: #fff;
  font-weight: 400;
  text-transform: uppercase;
}

.basket-table__header th {
  padding: 2rem 1rem;
  font-weight: 400;
  text-align: center;
  border: 0;
}

.basket-table__header th:first-child {
  text-align: left;
  padding-left: 5rem;
}

.basket-table__header th:last-child {
  padding-right: 5rem;
}

.basket-table__body td {
  padding: 3rem 2rem;
  text-align: center;
}

.basket-table__body td:first-child {
  text-align: left;
  padding-left: 5rem;
}

.basket-table__body td:last-child {
  padding-right: 5rem;
}

.basket-table__empty {
  text-align: center;
  color: #a7a7a7;
}
</style>
