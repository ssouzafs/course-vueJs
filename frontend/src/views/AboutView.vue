<script setup>
import { onUnmounted } from 'vue';
/** 
 * Utilizado para parar a montagem de component. Nesse exemplo o o método setInterval() é chamado no mounted
 * a cada 1 seg. E nesse caso mesmo que entre em outra página o método continua a ser chamado. è aí que entra o
 * onmonted(), pois a execução dentro do mesmo pode ser implementada a parada do método do mounted()
 */
onUnmounted(() => {
  console.log('onUnmounted Successfull!!!')
})

</script>
<template>
  <div class="about">
    <h1>Sobre</h1>
  </div>
</template>

