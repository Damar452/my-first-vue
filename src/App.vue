
<script setup>
import { ref, computed } from 'vue';

const name = 'Vue Dinamico';

const counter = ref(0);
const favoriteNumbers = ref([]);

const increment = () => counter.value++;
const decrement = () => counter.value--;
const reset = () => counter.value = 0;

const classCounter = computed(() => {
  if (counter.value === 0) return '';
  return counter.value > 0 ? 'green' : 'red';
})

const addNumber = () => favoriteNumbers.value.push(counter.value);

const hasNumber = computed(() => {
  const number = favoriteNumbers.value.find(number => number === counter.value);
  return number === 0 ? true : number;
});

</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>

    <div class="btn-group">
      <button @click="decrement" class="btn btn-danger">Decrementar</button>
      <button @click="reset" class="btn btn-secondary">Reset</button>
      <button @click="increment" class="btn btn-success">Incrementar</button>
      <button @click="addNumber" :disabled="hasNumber" class="btn btn-primary">Agregar favorito</button>
    </div>


    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(number, index) in favoriteNumbers" :key="index">{{ number }}</li>
    </ul>
  </div>
</template>

<style>

.red {
  color: red
}

.green {
  color: green
}

</style>