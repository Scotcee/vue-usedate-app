<template>
  <div>
    <h1>{{ useDate }}</h1>
  </div>
  <div>
    <button @click="addDay">Add Day</button>
    <button @click="addMonth">Add Month</button>
    <button @click="resetDate">Reset</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const originalDate = new Date();
const currentDate = ref(new Date());
const useDate = ref(currentDate.value.toDateString());

const addDay = () => {
  const lastDayOfMonth = new Date(
    currentDate.value.getFullYear(),
    currentDate.value.getMonth() + 1,
    0
  ).getDate();

  if (currentDate.value.getDate() + 1 > lastDayOfMonth) {
    currentDate.value.setMonth(currentDate.value.getMonth() + 1);
    currentDate.value.setDate(1);
  } else {
    currentDate.value.setDate(currentDate.value.getDate() + 1);
  }

  useDate.value = currentDate.value.toDateString();
};

const addMonth = () => {
  if (currentDate.value.getMonth() + 1 > 11) {
    currentDate.value.setFullYear(currentDate.value.getFullYear() + 1);
    currentDate.value.setMonth(0);
  } else {
    currentDate.value.setMonth(currentDate.value.getMonth() + 1);
  }

  useDate.value = currentDate.value.toDateString();
};

const resetDate = () => {
  currentDate.value = new Date(originalDate);
  useDate.value = currentDate.value.toDateString();
};
</script>

<style scoped>
/* Your scoped styles here */
</style>
