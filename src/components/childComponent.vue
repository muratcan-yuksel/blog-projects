<template>
  <div class="card">
    <div class="para">{{ data.name }} {{ data.surName }}</div>
  </div>
</template>

<script setup>
const props = defineProps({
  data: { required: true, type: Object },
});
</script>

<style scoped>
.card {
  margin-bottom: 1rem;
  /* border: 5px solid green; */
  text-align: center;
  width: 250px;
  height: 50px;
  border-radius: 16px;
}
.para {
  font-weight: 700;
}
</style>
