<template>
  <Header
    :carrito="carrito"
    @incrementar-cantidad="incrementarCantidad"
    @decrementar-cantidad="decrementarCantidad"
  ></Header>
  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>

    <div class="row mt-5">
      <Guitarra
        v-for="guitarra in guitarras"
        :guitarra="guitarra"
        @agregar-carrito="agregarCarrito"
      />
    </div>
  </main>
  <Footer></Footer>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { db } from "./data/guitarras";
import Guitarra from "./components/Guitarra.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

const guitarras = ref([db]);
const carrito = ref([]);

onMounted(() => {
  guitarras.value = db;
});

const agregarCarrito = (guitarra) => {
  const existeCarrito = carrito.value.findIndex(
    (producto) => producto.id === guitarra.id
  ); //Si un elemento existe o no en el arreglo mostrando su posicion
  if (existeCarrito >= 0) {
    carrito.value[existeCarrito].cantidad++;
  } else {
    guitarra.cantidad = 1;
    carrito.value.push(guitarra); //.push agrega un objeto al final de un array
  }
};

const decrementarCantidad = () => {
  alert('Quitar')
};

const incrementarCantidad = () => {
  alert('Dar')
};
</script>

<style scoped>
h1 {
  text-transform: uppercase;
  color: red;
}
</style>
