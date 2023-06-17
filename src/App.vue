<template>
  <Header
    :carrito="carrito"
    :guitarra="guitarra"
    @agregar-carrito="agregarCarrito"
    @incrementar-cantidad="incrementarCantidad"
    @decrementar-cantidad="decrementarCantidad"
    @eliminar-producto="eliminarProducto"
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
const guitarra = ref({});

onMounted(() => {
  guitarras.value = db;
  guitarra.value = db[3];
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

const decrementarCantidad = (id) => {
  const index = carrito.value.findIndex(producto => producto.id === id);
  if (carrito.value[index].cantidad <=1  ) return;
  carrito.value[index].cantidad--;
};

const incrementarCantidad = (id) => {
  const index = carrito.value.findIndex(producto => producto.id === id);
  if (carrito.value[index].cantidad >=5  ) return;
  carrito.value[index].cantidad++;
};

const eliminarProducto = (id) => {
  carrito.value = carrito.value.filter(producto => producto.id !== id);
};
</script>

<style scoped>
h1 {
  text-transform: uppercase;
  color: red;
}
</style>
