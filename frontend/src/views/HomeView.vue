<template>
  <h2>Home</h2>
  <hr />
  <button @click="modal.open = !modal.open">Open modal</button>

  <template v-if="modal.open">
    <Modal>
      <template #header>
        <h4>Cabeçalho</h4>
      </template>
      <template #default>
        <form action="">
            <h4>Conteudo</h4>
            <input type="text"><br>
            <input type="text"><br>
            <input type="text"><br>
            <input type="text"><br>
        </form>
      </template>
      
      <template #footer>
        <h4>Rodapé</h4>
      </template>
    </Modal>
  </template>
</template>

<script setup>
import { reactive } from "vue";
import Modal from "@/components/Modal.vue";

const modal = reactive({ open: false });
</script>

