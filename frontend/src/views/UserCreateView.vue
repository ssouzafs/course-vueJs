<template>
  <ul>
    <h3>Administradores</h3>
    <template v-for="(user, index) in users.data" :key="index">
      <li v-if="user.is_admin">{{ user.first_name }}</li>
    </template>
  </ul>
  <hr />
  <ul>
    <h3>Usuários</h3>
    <template v-for="(user, index) in usersNotAdmins" :key="index">
      <li> {{ user.first_name }}</li>
    </template>
  </ul>
  <hr>
  <p> Propriedade Compudata: 
    {{ countComputed }}
  </p>
  <p> function:
    {{ countFunction() }}
  </p>
  <button @click="computedCount++">Add Computed</button> <button @click="functionCount++">Function Count</button>
  <br>
</template>

<script setup>

import { api } from "@/services/api.js";
import { reactive, computed, ref } from "vue";

const users = reactive({data:[]});
const computedCount = ref(0);
const functionCount = ref(0);

const usersNotAdmins = computed(() => {
  return users.data.filter((user) => user.is_admin === 0);
});

const countComputed = computed(() => {
  console.log('Chamando computed Count')
  return  computedCount.value
})

function countFunction() {
  console.log('Chamando Function Count')
  return functionCount.value
}

api
  .get("api/users")
  .then((res) => {
    users.data = res.data;
  })
  .catch((error) => {
    console.log("Error: " + error.response.data);
  });
</script>