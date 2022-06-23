<template>
  <nav>
    <router-link to="/" class="nav-item">Home</router-link>
    <router-link to="/about" class="nav-item">About</router-link>
    <router-link to="/user/create" class="nav-item">New user</router-link>
  </nav>
</template>
<script>

</script>

<style scoped>
nav {
  display: flex;
  height: 30px;
  background-color: black;
  padding: 10px;
  align-items: center;
}

nav .nav-item {
  padding: 10px;
  color:white;
}

</style>