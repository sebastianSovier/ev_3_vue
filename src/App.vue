<script setup lang="ts">
import Ejercicio1 from './components/Ejercicio1.vue'
import img1 from './assets/img1.jpeg'
import img2 from './assets/img2.jpg'
import img3 from './assets/img3.jpeg'
import img4 from './assets/img4.jpeg'
import img5 from './assets/img5.jpeg'
import img6 from './assets/img6.jpeg'

const gridColumns = ['nombre', 'precio', 'img']
const gridData = [
  { nombre: 'Audifono', precio: 30000, stock: 3, img: img1 },
  { nombre: 'Mouse', precio: 20000, stock: 5, img: img2 },
  { nombre: 'Teclado', precio: 15000, stock: 10, img: img3 },
  { nombre: 'Gabinete', precio: 35000, stock: 4, img: img4 },
  { nombre: 'Pantalla', precio: 175000, stock: 3, img: img5 },
  { nombre: 'Silla', precio: 150000, stock: 2, img: img6 }
]
</script>

<template>
  <Ejercicio1 :data="gridData" :columns="gridColumns"></Ejercicio1>
</template>
