<script setup lang="ts">
import { ref, onMounted } from "vue";
import type { Employee } from "../types/employee";

interface ApiUser {
  id: number;
  name: string;
}
const employees = ref<Employee[]>([]);
const users = ref<ApiUser[]>([]);
const isLoading = ref(true);
const errorMessage = ref("");

async function fetchUser() {
  isLoading.value = true;
  errorMessage.value = "";

  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    if (!response.ok) {
      throw new Error(`Request failed with status ${response.status}`);
    }
    const responseUser: ApiUser[] = await response.json();
    users.value = responseUser;
  } catch (error) {
    errorMessage.value =
      error instanceof Error ? error.message : "Failed to load employees";
  } finally {
    isLoading.value = false;
  }
}

onMounted(fetchUser);
</script>

<template>
  <div class="employees-view">
    <h1>Employees</h1>

    <!-- add form input receive employee Id and employee Name , -->

    <!-- display list of employee employees -->
  </div>
  <div class="employees-view">
    <h1>User</h1>
    <!-- display user fetch api  -->
  </div>
</template>

<style scoped>
.employees-view {
  max-width: 960px;
  margin: 0 auto;
  padding: 2rem 1rem;
  text-align: left;
}

.error {
  color: #d33;
}

.card-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 1rem;
  margin-top: 1.5rem;
}

.card {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
}

.card-id {
  font-size: 0.8rem;
  color: #888;
}

.card-name {
  font-size: 1.1rem;
  font-weight: 600;
}
</style>
