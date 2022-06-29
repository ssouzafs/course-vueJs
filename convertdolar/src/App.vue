<template>
  <h2>App</h2>
  <hr>
  <div class="container">
    <div class="p-3 bg-light shadow">
      <div class="form-group mb-2">
        <p class="dollar">Dólar hoje: <span> {{ showDollarToday }}</span> </p>
        <Currency type="text" class="form-control" placeholder="Informe o valor em dólar..." v-model="inputDollar"
          :options="{ currency: 'USD' }" />
      </div>
      <p class="dollar-in-real">{{ showDollarToReal }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, computed, onMounted } from 'vue';
import { formatter } from '@/services/formatter';
import { api } from '@/services/api';
import Currency from '@/components/Currency';
const inputDollar = ref(0);
const grossDollar = ref(0);
const dollarToReal = ref(0);

const showDollarToReal = computed(() => {
  return formatter(dollarToReal.value, 'pt-BR', 'BRL');
});

const showDollarToday = computed(() => {
  return formatter(grossDollar.value, 'en-US', 'USD');
})

onMounted(async () => {
  try {
    const rawCurrency = await getCurrentDolar();
    grossDollar.value = rawCurrency.high;
  } catch (err) {
    console.log("Error: " + err.response.data);
  }
})

async function getCurrentDolar(currencyTpe = 'USD-BRL') {
  const { data } = await api.get(`https://economia.awesomeapi.com.br/json/last/${currencyTpe}`);
  const currencySplited = currencyTpe.split('-').join('');
  return data[currencySplited];
}

watch(inputDollar, (value) => {
  dollarToReal.value = value * Number(grossDollar.value);
})
</script>

<style scoped>

input {
   font-weight: 300;
}
.dollar-in-real {
  padding: 8px;
  border-radius: 3px;
  color: rgb(47, 168, 128);
  border: 1px solid rgb(47, 168, 128);
  text-align: center;
}
.dollar {
  font-weight: 300;
}

.dollar span {
  color: rgb(235, 32, 116);
  font-weight: 400;
}
</style>