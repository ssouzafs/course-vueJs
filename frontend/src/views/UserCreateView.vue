<template>
  <div>
    <form action="">
      <input
        type="text"
        v-model="user.first_name"
        placeholder="Primeiro nome"
      />
      <span v-if="errors['first_name']">{{ errors["first_name"][0] }}</span>
      <br />

      <input type="text" v-model="user.last_name" placeholder="Segundo nome" />
      <span v-if="errors['last_name']">{{ errors["last_name"][0] }}</span
      ><br />

      <input type="text" v-model="user.password" placeholder="Senha" />
      <span v-if="errors['password']">{{ errors["password"][0] }}</span
      ><br />

      <input type="text" v-model="user.email" placeholder="E-mail" />
      <span v-if="errors['email']">{{ errors["email"][0] }}</span
      ><br />

      <button @click.prevent="createUser">Cadastrar</button>
    </form>

    <p>{{ fullName }}</p>
  </div>
</template>

<script setup>
import { api } from "@/services/api.js";
import { ref, computed } from "vue";

const user = ref({});
const errors = ref([]);

async function createUser() {
  await api
    .post("/api/users/store", user)
    .then((response) => {
      console.log(response.data);
    })
    .catch((err) => {
      if (err.response?.data) {
        errors.value = err.response.data["errors"];
      }

      console.log(errors.value);
    });
}

const fullName = computed(()=> {
    return user.first_name + ' ' + user.last_name
})
</script>
<style scoped>
div {
  width: 100%;
  padding: 10px;
}

input {
  margin: 2px;
  height: 20px;
  padding: 5px;
}

span {
  display: block;
  color: brown;
  font-size: 0.8rem;
}
button {
  margin-top: 5px;
  padding: 6px 12px;
  background: rgba(49, 134, 95, 0.61);
  color: white;
  border: none;
  border-radius: 3px;
}
</style>