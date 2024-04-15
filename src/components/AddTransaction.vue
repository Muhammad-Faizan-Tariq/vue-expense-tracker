<template>
  <div class="px-8 my-6">
    <div class="my-4 border-b w-full">
      <h2 class="font-semibold text-lg">Add new transaction</h2>
    </div>
    <div class="bg-white p-4 border-2 rounded-md">
      <form id="form" @submit.prevent="onSubmit">
        <div class="my-5 text-sm">
          <label for="text" class="block text-black">Text</label>
          <input
            type="text"
            id="text"
            v-model="text"
            autofocus
            class="rounded-sm px-4 py-3 mt-1 focus:outline-none bg-gray-100 w-full"
            placeholder="Enter Text"
          />
        </div>
        <div class="my-5 text-sm">
          <label for="amount" class="block text-black">
            Amount
            <small class="text-gray-600">
              (
              <span class="text-red-400"> negative-expense</span> ,
              <span class="text-green-400"> positive-income</span>
              )
            </small>
          </label>
          <input
            type="text"
            id="amount"
            v-model="amount"
            autofocus
            class="rounded-sm px-4 py-3 mt-1 focus:outline-none bg-gray-100 w-full"
            placeholder="Enter Amount"
          />
        </div>
        <div class="my-5">
          <button
            class="rounded-sm block text-center text-white bg-gray-800 p-3 duration-300 hover:bg-black w-full"
          >
            Add Transaction
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const text = ref("");
const amount = ref("");
const toast = useToast();
const emit = defineEmits(["transactionSubmitted"])

const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error("Both field are required");
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value)
  }

  emit("transactionSubmitted", transactionData)
  text.value = "";
  amount.value = "";
};
</script>
