<template>
  <h2>App</h2>
  <hr>
  <div class="container">
    <div class="p-3 bg-light shadow">
      <div class="form-group mb-2">
        <input type="text" class="form-control" placeholder="Nome..." v-model="user.firstName" />
      </div>
      <div class="form-group mb-2">
        <input type="text" class="form-control" placeholder="Sobrenome..." v-model="lastName" />
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref, watchEffect } from 'vue';

const firstName = ref('');
const lastName = ref('');
const user = ref({
  firstName: '',
  lastName: ''
})

const items = ref([
  {
    id: 1,
    name: 'sergio'
  },
  {
    id: 2,
    name: 'Maria'
  },
])

/** Tipos Primitivos */
// watch([firstName, lastName], ([valueFirstName, valueLastName], [oldFirstName, oldLastName]) => {
//   console.log('New Value: ' + valueLastName);
//   console.log('Old Value: ' + oldLastName);
// })

/** Objetos */
watchEffect(() => {
  console.log('É carregado antes de carregar o DOM. Fica ouvindo tudo.')
})
</script>