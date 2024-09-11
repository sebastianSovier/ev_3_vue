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

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: inline;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
