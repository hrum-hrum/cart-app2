<script setup>
defineProps({
  totalPrice: {
    type: Number,
    default: 0,
  },
})

function priceInUSD(sum) {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
  }).format(sum)
}
</script>

<template>
  <td colspan="5">
    <div class="basket-table__summary">
      <p class="basket-table__total">
        Total <b>{{ priceInUSD(totalPrice) }}</b>
      </p>
      <p>Tax {{ priceInUSD(totalPrice * 0.1) }}</p>
    </div>
  </td>
</template>

<style>
.basket-table__summary {
  text-align: right;
}

.basket-table__total {
  font-size: 1.4rem;
}
</style>
