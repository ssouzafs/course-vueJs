<template>
  <h2>App</h2>
  <hr>
  <div class="container">
    <div class="p-3 bg-light shadow">
      <div class="form-group mb-2">
        <Currency type="text" class="form-control" placeholder="Valor..." v-model="inputDolar"
          :options="{ currency: 'USD' }" />
      </div>
      <p>Dólar hoje: </p>
      <p>Valor em reais: {{ dolarFormatedBrl }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, computed, onMounted } from 'vue';
import { formatter } from '@/services/formatter';
import { api } from '@/services/api';
import Currency from '@/components/Currency';
const inputDolar = ref(0);
const dolarToday = ref(0);

const dolarFormatedBrl = computed(() => {
  return formatter(inputDolar.value, 'en-US', 'USD');
});

const dolarTodayValue = computed(() => {

})

onMounted(() => {
  getCurrentDolar();
})

async function getCurrentDolar(currencyTpe = 'USD-BRL') {
  await api.get(`https://economia.awesomeapi.com.br/json/last/${currencyTpe}`)
    .then((response) => {
      const currencySplited = currencyTpe.split('-').join('');
      return response.data[currencySplited];
    }).catch((error) => {
      console.log(error.response.data)
    });
}

</script>