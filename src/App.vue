<template>
  <div class="flex justify-center items-center">
    <div class="max-w-lg w-full">
      <Header />
      <Balance :total="+total" />
      <IncomeExpenses :income="+income" :expense="+expense" />
      <TransactionList :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted" />
      <AddTransaction @transactionSubmitted="handleSubmitTransaction" />
    </div>
  </div>
</template>

<script setup>
import AddTransaction from "./components/AddTransaction.vue";
import Balance from "./components/Balance.vue";
import Header from "./components/Header.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import { ref, computed } from "vue";
import {useToast} from "vue-toastification";

const transactions = ref([
  { id: 1, text: "Flower", amount: -23 },
  { id: 2, text: "Salary", amount: 700 },
  { id: 3, text: "Register", amount: -90 },
  { id: 4, text: "Amount", amount: 123 },
]);

const toast = useToast()

const total = computed(() => {
  return transactions.value
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

const handleSubmitTransaction = (transactionData) => {
    console.log("Transaction Data:", transactionData)
    transactions.value.push({
      id: generateUniqueId(),
      text: transactionData.text,
      amount: transactionData.amount
    });
    toast.success("Transaction Added")
}

const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000)
}

const handleTransactionDeleted = (id) => {
  console.log(id)
  transactions.value = transactions.value.filter((transaction)=>
    transaction.id !== id
  )
  toast.success("Transaction deleted")
}
</script>
