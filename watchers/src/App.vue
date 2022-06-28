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
import { ref, watch } from 'vue';

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
watch(
  /** uma propriedade do objeto */
  // () => user.value.firstName,
  // (value, oldValue) => {
  //   console.log(value, oldValue)
  // }

  /** o objeto como um todo */
  // () => user,
  // (value, oldValue) => {
  //   console.log(value, oldValue)
  // }

  /** Array */
  items, (value) => {
    value.forEach(item => {
      if (!Number.isInteger(Number(item))) {
        console.log(`${item.name} não é um número`)
      }
    })
  }
)
</script>