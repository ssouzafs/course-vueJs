<template>
  <h1>APP</h1>
  <input type="text"  v-model="userName"/>

  <select v-model="userName">
    <option :value="user.fullName" v-for="user in users" :key="{user}">{{ user.fullName}}</option>
  </select>
  <br>
  <template v-for="user in users" :key="{user}">
    <input @click="userName = user.fullName" :checked="userName === user.fullName" type="checkbox"/> {{ user.fullName}}
  </template>

  <br>
  
</template>

<script setup>
import { ref, onMounted, computed, onUpdated } from "vue";

const userName = ref('Sérgio')
const users = ref([
  {
    id: 0,
    fullName: 'Maria de Sá'
  },

    {
    id: 1,
    fullName: 'joão da Silva'
  },

    {
    id: 3,
    fullName: 'Graciela Moreira'
  }
])

</script>

<style scoped>
.color-danger {
  color: rgb(226, 29, 29);
}

.color-success {
  color: rgb(63, 202, 63);
}
</style>
