<template>
  <div class="flex space-x-0 flex-col lg:flex-row lg:space-x-2 my-2 px-6">
    <div
      class="bg-green-600 p-4 border-2 rounded-md shadow-lg w-full text-white text-center"
    >
      <h1 class="text-xl font-light">INCOME</h1>
      <h1 class="text-2xl text-green-100 font-semibold">PKR {{ income }}</h1>
    </div>
    <div
      class="bg-red-600 p-4 border-2 rounded-md shadow-lg w-full text-white text-center"
    >
      <h1 class="text-xl font-light">EXPENSE</h1>
      <h1 class="text-2xl text-red-100 font-semibold">PKR {{ expense }}</h1>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expense: {
    type: Number,
    required: true,
  },
});
</script>
