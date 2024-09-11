<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  data: Array,
  columns: Array
})

const cartItems = ref([])

const filteredData = computed(() => {
  let { data } = props
  return data
})

function agregar1Carrito(item) {
  const existingItem = cartItems.value.find((cartItem) => cartItem.nombre === item.nombre)

  if (existingItem) {
    if (existingItem.stock <= 0) {
      alert('No hay más unidades disponibles en stock')
      return
    }

    existingItem.quantity++
    existingItem.stock--
  } else {
    if (item.stock <= 0) {
      alert('No hay más unidades disponibles en stock')
      return
    }

    cartItems.value.push({ ...item, quantity: 1, stock: item.stock - 1 })
  }
}

function delete1Item(item) {
  const index = cartItems.value.findIndex((cartItem) => cartItem.nombre === item.nombre)

  if (index !== -1) {
    cartItems.value[index].stock++

    if (cartItems.value[index].quantity > 1) {
      cartItems.value[index].quantity--
    } else {
      cartItems.value.splice(index, 1)
    }
  }
}

const totalPrice = computed(() => {
  return cartItems.value.reduce((sum, item) => sum + item.precio * item.quantity, 0)
})
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <h2 class="text-center mb-4">Productos disponibles</h2>
        <div v-for="(item1, index) in filteredData" :key="index" class="mb-3 card">
          <div class="d-flex align-items-center">
            <img :src="item1.img" alt="product image" width="80" height="80" class="me-3" />
            <div class="me-auto">
              <h5>{{ item1.nombre }} - Precio $: {{ item1.precio }}</h5>
              <p>Stock: {{ item1.stock }}</p>
            </div>
            <button class="btn btn-primary" @click="agregar1Carrito(item1)">
              <i class="bi bi-cart"></i> Agregar al carrito
            </button>
          </div>
        </div>
      </div>

      <div class="col-md-6">
        <h2 class="text-center mb-4">Productos en el carrito</h2>
        <div v-if="cartItems.length">
          <div v-for="(item, index) in cartItems" :key="index" class="mb-3 card">
            <div class="d-flex align-items-center">
              <img :src="item.img" alt="cart item image" width="80" height="80" class="me-3" />
              <div class="me-auto">
                <h5>{{ item.nombre }} - Cantidad: {{ item.quantity }}</h5>
                <p>Stock restante: {{ item.stock }}</p>
              </div>
              <button class="btn btn-danger" @click="delete1Item(item)">
                <i class="bi bi-trash"></i> Remover del carrito
              </button>
            </div>
          </div>
        </div>
        <p v-else>El carrito está vacío.</p>
      </div>
    </div>

    <div class="mt-5 text-center">
      <h3>Total a pagar: ${{ totalPrice }}</h3>
    </div>
  </div>
</template>
