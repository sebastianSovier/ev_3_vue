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
function capitalize(str) {
  return str.charAt(0).toUpperCase() + str.slice(1)
}

function agregar1Carrito(item) {
  let marca = false
  let stockLess = false
  const existingItem = cartItems.value.find((cartItem) => cartItem.nombre === item.nombre)
  if (existingItem) {
    existingItem.quantity++
  } else {
    cartItems.value.push({ ...item, quantity: 1 })
  }

  cartItems.value.forEach((element) => {
    if (stockLess) {
      return
    }
    if (element.nombre === item.nombre) {
      element.stock -= 1
      stockLess = true
    }
    if (element.stock <= 0 && element.nombre === item.nombre) {
      marca = true
    }
  })
  if (marca) {
    alert('no hay mas unidades disponibles en stock')
  }
}

function delete1Item(item) {
  let stockAdd = false

  cartItems.value.forEach((element) => {
    if (stockAdd) {
      return
    }
    if (element.nombre === item.nombre) {
      element.stock += 1
      stockAdd = true
    }
  })
  const index = cartItems.value.findIndex((cartItem) => cartItem.nombre === item.nombre)
  if (index !== -1) {
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
  <div>
    <!-- Product Table -->
    <h2>Productos Disponibles</h2>
    <table v-if="filteredData.length">
      <thead>
        <tr>
          <th v-for="(item, index) in columns" :key="index">
            {{ capitalize(item) }}
          </th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item1, index) in filteredData" :key="index">
          <td v-for="(item, index) in columns" :key="index">
            <!-- Handle the image field specifically -->
            <img
              v-if="item === 'img'"
              :src="item1.img"
              :alt="`Imagen ${index + 1}`"
              width="100"
              height="100"
            />
            <!-- Display other fields normally -->
            <span v-else>{{ item1[item] }}</span>
          </td>
          <td>
            <button @click="agregar1Carrito(item1)">Agregar al carrito</button>
          </td>
        </tr>
      </tbody>
    </table>
    <p v-else>No matches found.</p>
    <!-- Cart Table -->
    <h2>Carrito</h2>
    <table v-if="cartItems.length">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Precio</th>
          <th>Cantidad</th>
          <th>Imagen</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in cartItems" :key="index">
          <td>{{ item.nombre }}</td>
          <td>{{ item.precio }}</td>
          <td>{{ item.quantity }}</td>
          <td>
            <img :src="item.img" :alt="`Carrito Imagen ${index + 1}`" width="100" height="100" />
          </td>
          <td><button @click="delete1Item(item)">Remover del carrito</button></td>
        </tr>
      </tbody>
    </table>
    <p v-else>El carrito está vacío.</p>

    <!-- Total Price -->
    <h3>Total: {{ totalPrice }}</h3>
  </div>
</template>
