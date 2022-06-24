<template>
  <p>Likes: {{ likes }}</p>
  <p>Comments: {{ comments }}</p>
</template>
<script setup>
defineProps({
    comments: Number,
    likes: Number,
});
</script>