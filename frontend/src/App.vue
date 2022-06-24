<template>
  <Nav />

  <router-view></router-view>
  <p>{{ counter.count }}</p>

  <button @click="counter.count++">Add count</button>
  <CountChild @increment="(value) => counter.count+= value"/>
</template>

<script setup>
import { reactive } from "vue";

import Nav from "@/components/Nav.vue";
import CountChild from "@/components/CountChild.vue";

const counter = reactive({ count: 0 });
</script>