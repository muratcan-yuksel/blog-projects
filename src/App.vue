<template>
  <div class="app">
    <!-- <h1 class="title">Characters</h1> -->
    <div
      v-for="(item, key) in data"
      :key="key"
      class="card"
      @click="handleClick(item)"
      :class="{
        greenBorder: item.isComing,
        // anotherClassName: item.anotherCondition,
      }"
    >
      <div class="para">{{ item.name }} {{ item.surName }}</div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from "vue";
import axios from "axios";
import childComponent from "./components/childComponent.vue";

const data = ref();
const changedData = ref();

const getData = async () => {
  try {
    const res = await axios.get("../public/data/data.json");
    console.log(res.data);
    data.value = res.data.items;
    changedData.value = res.data.items.map((item) => ({
      ...item,
      isGoing: false,
    }));
    console.log(res.data.items);
    console.log(changedData.value);
  } catch (error) {
    console.log(error);
  }
};

// const changeData = () => {
//   let newArr = data.value.map((item) => {
//     item["isGoing"] = false;
//   });
//   console.log(newArr);
// };

onMounted(() => {
  getData();
});
</script>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  /* justify-content: center; */
  align-items: center;
  padding-top: 5rem;
}
.card {
  margin-bottom: 1rem;
  /* border: 5px solid green; */
  text-align: center;
  width: 250px;
  height: 50px;
  border-radius: 16px;
  background-color: #ffe01b;
}
.para {
  font-weight: 700;
}
</style>
