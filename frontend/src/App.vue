<template>

  <div class="container-content">
    <section class="list">
      <h1 class="my-3">Listagem de Usuários</h1>
      <hr>
      <div class="d-flex justify-content-end mb-2">
        <input type="text" placeholder="Pesquisar..." v-model="filterInput" @keyup="filterInputDebounce">
      </div>
      <table class="table table-hover">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Nome Completo</th>
            <th scope="col">E-mail</th>
            <th scope="col">Data de Criação</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(user, index) in users.data" :key="index">
            <th scope="row">{{ user.id }}</th>
            <td>{{ user.first_name }} {{ user.last_name }}</td>
            <td>{{ user.email }}</td>
            <td>{{ dateFormatBrl(user.created_at) }}</td>
          </tr>
        </tbody>
      </table>
      <Pagination :data="users" @pagination-change-page="resolveEventPagination" align="center">
        <template #prev-nav>
          <span>&lt; &lt;</span>
        </template>
        <template #next-nav>
          <span>&gt;&gt;</span>
        </template>
      </Pagination>
    </section>
  </div>

</template>
<script setup>
import { ref, onMounted, computed } from 'vue';
import { api } from '@/services/api';
import _ from 'lodash';
import moment from 'moment';
import Pagination from 'laravel-vue-pagination';
const users = ref([]);
const filterInput = ref('');

onMounted(() => {
  getUsers();
})

function resolveEventPagination(page) {
  return inputFilterIsEmpty() ? getUsers(page) : getUsersByFilter(page);
}

function inputFilterIsEmpty() {
  return filterInput.value.length === 0;
}

const filterInputDebounce = _.debounce(() => {
  getUsersByFilter();
}, 750)

async function getUsersByFilter(page = 1) {
  await api.get(`/api/users?page=${page}`, {
    params: {
      user: filterInput.value
    }
  }).then((response) => {
    if (filterInput.value) {
      users.value = response.data;
      return;
    }
    getUsers();
  }).catch((error) => {
    console.log('Erro => ' + error.response.data)
  });
}

async function getUsers(page = 1) {
  await api.get(`/api/users?page=${page}`).then((response) => {
    users.value = response.data;
  }).catch((error) => {
    console.log('Erro => ' + error.response.data)
  });
}

function dateFormatBrl(date, format = 'DD/MM/YYYY h:mm:ss') {
  return date ? moment(date).format(format) : null;
}

</script>

<style scoped>
.container-content {
  width: 100%;
  margin: 20px;
}

section.list {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  max-width: 1140px;
  margin: 0 auto;
  padding: 20px;
  background-color: #FFF;
}

section.list h1 {
  font-size: 1.3rem;
  font-weight: 300;
}

section.list input {
  font-size: .775rem;
  font-weight: 300;
  height: 30px;
}

section.list input::placeholder {
  font-size: .775rem;
}
</style>