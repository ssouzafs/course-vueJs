<template>
  <div class="container">
    <h2>App</h2>
    <hr>
    <div class="form-control">
      <button @click="showSomething">Toggle Element</button>
      <input type="text" v-if="toggleElement" ref="inputElement">
    </div>
  </div>
</template>

<script setup>
import { nextTick, ref } from 'vue';
const toggleElement = ref(false);
const inputElement = ref(null);

function showSomething() {
  toggleElement.value = !toggleElement.value
  // toggleElement.value = true;

  /** Precisa do setTimeOut porque o elemento ainda não está renderizado para ser capturado */
  // setTimeout(() => {
  //   console.log(inputElement.value)
  // }, 100)

  /**
   *  Solução mais plausivel é utilizar o nextTick 
   *  Neste caso o conteúdo é carregado por último, no exemplo abaixo
   * o log 'depois do focus' é carregado primeiro. Caso queremos que o conteúdo do 
   * nextTick seja carregado primeiro, basta usar o recurso de async e await
  */
  if (toggleElement.value) {
    nextTick(() => {
      inputElement.value.focus();
    })
  }
  console.log("Depois do Focus")

}
</script>