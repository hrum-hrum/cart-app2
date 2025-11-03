<script setup>
import { reactive, computed } from 'vue'
import BasketTable from './components/BasketTable.vue'

const basket = reactive([
  {
    id: 1,
    name: 'Blue Flower Print Crop Top',
    color: 'Yellow',
    size: 'M',
    price: 29.0,
    quantity: 1,
    imageUrl: './assets/crop-top.png',
  },
  {
    id: 2,
    name: 'Levender Hoodie',
    color: 'Levender',
    size: 'XXL',
    price: 119.0,
    quantity: 1,
    imageUrl: './assets/hoodie.png',
  },
  {
    id: 3,
    name: 'Black Sweatshirt',
    color: 'Black',
    size: 'XXL',
    price: 123.0,
    quantity: 1,
    imageUrl: './assets/crop-top.png',
  },
])

const increaseItemQuantity = (item) => {
  item.quantity++
}

const decreaseItemQuantity = (item) => {
  if (item.quantity > 0) {
    item.quantity--
  }
}

const removeItem = (index) => {
  basket.splice(index, 1)
}

const totalPrice = computed(() => {
  return basket.reduce((sum, item) => {
    return sum + item.price * item.quantity
  }, 0)
})
</script>

<template>
  <div class="container basket">
    <BasketTable
      :basket="basket"
      :total-price="totalPrice"
      @increase-item-quantity="increaseItemQuantity"
      @decrease-item-quantity="decreaseItemQuantity"
      @remove-item="removeItem"
    />
  </div>
</template>

<style src="./App.css"></style>
