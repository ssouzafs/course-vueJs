<template>
 <button @click="add">Incrementar Contador </button> 
</template>

<script setup>
const emit = defineEmits(['increment'])

function add() {
    emit('increment', 10)
}
</script>