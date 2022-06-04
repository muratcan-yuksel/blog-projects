<template>
  <div>
    <h1 class="title">The team</h1>
    <div class="card" v-for="(item, key) in data" :key="key"></div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import childComponent from "./components/childComponent.vue";

const data = [
  { name: "Anakin", surName: "Skywalker", isJedi: true },
  { name: "Padmé", surName: "Amidala", isJedi: false },
  { name: "Obi-Wan", surName: "Kenobi", isJedi: true },
];
</script>

<style scoped></style>
