<script setup lang="ts">
import type { Option } from "../src/types";

import { ref } from "vue";
import VueSelect from "../src/Select.vue";

type BookOption = Option<string>;
type UserOption = Option<number> & { username: string };

const activeBook = ref<string | null>(null);
const activeUsers = ref<number[]>([1, 3]);
const isLoading = ref(false);

const bookOptions: BookOption[] = [
  { label: "Alice's Adventures in Wonderland", value: "alice", groupName: "Group 1" },
  { label: "A Wizard of Earthsea", value: "wizard", groupName: "Group 2" },
  { label: "Harry Potter and the Philosopher's Stone", value: "harry_potter_1", groupName: "Group 1" },
  { label: "Harry Potter and the Chamber of Secrets", value: "harry_potter_2", groupName: "Group 2" },
];

const userOptions: UserOption[] = [
  { label: "Alice", value: 1, username: "alice" },
  { label: "Bob", value: 2, username: "bob" },
  { label: "Charlie", value: 3, username: "charlie" },
  { label: "David", value: 4, username: "david" },
  { label: "John", value: 5, username: "john" },
  { label: "Admin", value: 6, username: "admin" },
  { label: "Root", value: 6, username: "root" },
];
</script>

<template>
  <div class="container">
    <form class="form-container" @submit.prevent="null">
      
      <p>Non-grouped:</p>

      <VueSelect
        v-model="activeBook"
        :options="bookOptions"
        :is-multi="false"
        :is-loading="isLoading"
        placeholder="Pick a book"
      />

      <p>Grouped:</p>

      <VueSelect
        v-model="activeBook"
        :isGrouped="true"
        :options="bookOptions"
        :is-multi="false"
        :is-loading="isLoading"
        placeholder="Pick a book"
      />

      <p class="selected-value">
        Selected book value: {{ activeBook || "none" }}
      </p>

      <VueSelect
        v-model="activeUsers"
        :options="userOptions"
        :is-multi="true"
        :is-loading="isLoading"
        placeholder="Pick users"
      />

      <p class="selected-value">
        Selected user value: {{ activeUsers || "none" }}
      </p>
    </form>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300..900&display=swap');

body {
  -webkit-font-smoothing: antialiased;
  margin: 0;
  font-family: "Inter", sans-serif;
}
</style>

<style lang="scss" scoped>
.container {
  min-height: calc(100vh - 4rem);
  padding: 2rem;
  background-color: #f4f4f5;

  .form-container {
    display: flex;
    flex-direction: column;
    max-width: 400px;
    padding: 2rem;
    margin: 0 auto;
    border-radius: 6px;
    background-color: #fff;

    .selected-value {
      font-size: 14px;
      font-weight: 500;
      font-family: "IBM Plex Mono", monospace;
    }
  }
}
</style>
