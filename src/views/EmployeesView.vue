<script setup lang="ts">
import { ref, computed, onMounted } from "vue";
import type { Employee } from "../types/employee";

interface ApiUser {
  id: number;
  name: string;
  username: string;
  email: string;
  phone: string;
  website: string;
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
    <h1>User</h1>
    <table class="user-table"></table>
  </div>
  <div class="employees-view">
    <h1>Employees</h1>

    <table class="user-table"></table>

    <button type="button" class="action-button">แสดงคนทั้งหมด</button>

    <button type="button" class="action-button">Total Salary</button>

    <button type="button" class="action-button">Max Salary</button>
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

.user-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 1rem;
}

.user-table th,
.user-table td {
  padding: 0.5rem 0.75rem;
  border: 1px solid #e0e0e0;
  text-align: left;
}

.user-table th {
  background-color: #f5f5f5;
  font-weight: 600;
}

.employee-form {
  display: flex;
  gap: 0.5rem;
  margin-top: 1rem;
  margin-bottom: 1rem;
}

.employee-form input {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.employee-form button {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  background-color: #42b883;
  color: #fff;
  cursor: pointer;
}

.employee-form button:hover {
  background-color: #369870;
}

.action-button {
  display: block;
  margin-top: 0.75rem;
  padding: 0.5rem 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: #fff;
  cursor: pointer;
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
