<template>
  <div class="px-8">
    <div class="my-4 border-b w-full">
      <h2 class="font-semibold text-lg">History</h2>
    </div>
    <div
      v-for="item in transactions"
      :key="item.id"
      :class="item.amount < 0 ? 'border-red-500' : 'border-green-500'"
      class="ml-6 relative bg-white p-4 border-r-8 shadow-md my-4 flex justify-between"
    >
      <div class="absolute -left-6">
        <button
          @click="deletedTransation(item.id)"
          class="cursor-pointer bg-red-600 p-2 w-6 flex items-center text-xs text-white justify-center"
        >
          x
        </button>
      </div>
      <div>
        <p>{{ item.text }}</p>
      </div>
      <div>
        <p>{{ item.amount }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const emit  = defineEmits(["transactionDeleted"])

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const deletedTransation = (id) => {
  emit("transactionDeleted", id)
}
</script>
