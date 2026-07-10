<script setup lang="ts"></script>

<template>
  <nav class="nav">
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/employees">Employees</RouterLink>
  </nav>

  <RouterView />
</template>

<style scoped>
.nav {
  display: flex;
  gap: 1rem;
  padding: 1rem;
  border-bottom: 1px solid #e0e0e0;
}
</style>
