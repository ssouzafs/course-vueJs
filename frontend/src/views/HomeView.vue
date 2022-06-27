<template>
  <div class="m-3">
    <input
      type="text"
      placeholder="Pesquisar"
      v-model="userSearch"
      @keyup="search"
    />
    <hr />
    <p class="result" v-for="(user, index) in users.data" :key="index">
      {{ user.first_name }} {{ user.last_name }}
    </p>
    <Pagination :data="users" @pagination-change-page="handleEventPagination">
      <template #prev-nav>
        <span>&lt; Anterior</span>
      </template>
      <template #next-nav>
        <span>Próximo &gt;</span>
      </template>
    </Pagination>
    <p class="not-found" v-if="userNotFound">Usuário não encontrado!</p>
  </div>
</template>
<script setup>
import { onMounted, ref, computed } from "vue";
import _ from "lodash";
import Pagination from "laravel-vue-pagination";
import { api } from "@/services/api";

const users = ref([]);
const userSearch = ref("");

async function getData(page = 1) {
  await api
    .get("/api/users?page=" + Number(page))
    .then((response) => {
      users.value = response.data;
    })
    .catch((err) => {
      console.log(err);
    });
}

onMounted(() => {
  getData();
});
async function searchUser(page = 1) {
  await api
    .get("/api/users/search?page=" + Number(page), {
      params: {
        user: userSearch.value,
      },
    })
    .then((response) => {
      if (!userSearch.value) {
        getData();
        return;
      }
      users.value = response.data;
      console.log(users.value.data);
    })
    .catch((err) => {
      console.log(err);
    });
}

function handleEventPagination(page) {
  return userSearch.value ? searchUser(page) : getData(page);
}

const search = _.debounce(async () => {
  searchUser();
}, 450);

const userNotFound = computed(() => {
  return users.value.data == 0;
});
</script>

<style scoped>
.not-found {
  border: 1px solid rgb(236, 40, 89);
  padding: 10px 5px;
  border-radius: 3px;
  opacity: 0.875;
  color: rgb(236, 40, 89);
}

.result {
  list-style: none;
  padding: 10px 5px;
  /* border-radius: 3px; */
  opacity: 0.875;
  margin: 10px 0;
  color: black;
  border-bottom: 1px solid gray;
}
</style>
