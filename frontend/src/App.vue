<script setup>
import _ from "lodash";
import { ref } from "vue";

// const search = ref('')
// function search() {
//   console.log('Teste')
// }
const search = _.debounce((value) => {
  console.log(value.target.value);
}, 1000);
</script>

<template>
  <router-view></router-view>
  <hr />
  <input type="text" placeholder="Search" @keyup="search" />
</template>