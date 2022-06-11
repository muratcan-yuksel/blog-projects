<template>
  <div class="app">
    <!-- <div
      v-for="(item, key) in changedData"
      :key="key"
      class="card"
      @click="handleClick(item)"
      :class="[item.isGoing ? 'going' : 'notGoing']"
    >
      <div class="para">{{ item.name }} {{ item.surName }}</div>
    </div> -->
    <child-component
      @click="handleClick(item)"
      :class="[item.isGoing ? 'going' : 'notGoing']"
      v-for="(item, key) in changedData"
      :key="key"
      :data="item"
    />
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
    changedData.value = res.data.items.map((item, index) => ({
      ...item,
      isGoing: false,
      data: index,
    }));
    console.log(res.data.items);
    console.log(changedData.value);
  } catch (error) {
    console.log(error);
  }
};

const handleClick = (item) => {
  item.isGoing = !item.isGoing;
  console.log(item);
};

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
}
.para {
  font-weight: 700;
}
.going {
  border: 5px solid green;
  text-decoration: none;
  background-color: rgb(56, 219, 56);
}
.notGoing {
  background-color: #ffe01b;
}
</style>
