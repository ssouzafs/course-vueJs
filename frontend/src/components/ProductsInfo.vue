<template>
  <ul>
    <slot v-for="product in products" key="product.id" :product="product"></slot>
  </ul>
</template>
<script setup>
defineProps({
  products: Object,
});
</script>