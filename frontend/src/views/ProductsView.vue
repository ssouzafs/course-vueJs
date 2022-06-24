<template>
  <h3>Produtos</h3>
  <hr />
  <p>
    Lorem, ipsum dolor sit amet consectetur adipisicing elit. Exercitationem,
    repellendus aliquid! Maiores, delectus porro aliquid nemo id fuga, esse odit
    qui officia saepe beatae.
  </p>
  <ProductsInfo :likes="product.likes" :comments="product.comments" />
</template>

<script setup>
import { reactive } from "vue";
import ProductsInfo from "@/components/ProductsInfo.vue";

const product = reactive({
  likes: 20,
  comments: 30,
});
</script>