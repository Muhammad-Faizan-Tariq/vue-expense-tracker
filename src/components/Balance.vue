<template>
  <div class="flex justify-center flex-col px-8 py-2">
    <h4 class="text-lg text-gray-500 font-thin">Your Balance</h4>
    <h4 class="text-2xl font-semibold">PKR {{ total }}</h4>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
});
</script>
