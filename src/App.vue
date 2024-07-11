<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { nanoid } from "nanoid";
import { useToast } from "vue-toastification";
import { computed, ref, onMounted } from "vue";

const toast = useToast();
const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

// Get total
const total = computed(() => {
  return parseFloat(
    transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
  );
});

// Get income
const income = computed(() => {
  return parseFloat(
    transactions.value
      .filter((transaction) => transaction.amount > 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0)
      .toFixed(2)
  );
});

// Get expenses
const expenses = computed(() => {
  return parseFloat(
    transactions.value
      .filter((transaction) => transaction.amount < 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0)
      .toFixed(2)
  );
});

// Add transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: nanoid(),
    text: transactionData.text,
    amount: transactionData.amount,
  });

  saveTransactionsToLocalStorage();

  toast.success("Transaction Added");
};

// Delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );

  saveTransactionsToLocalStorage();

  toast.success("Transaction deleted");
};

// Save transactions to local storage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>

<template>
  <div
    class="font-poppins w-full min-h-svh bg-stone-900 text-gray-200 flex items-center justify-center"
  >
    <div class="max-w-[400px] mx-auto px-2 py-5">
      <header>
        <Header />
      </header>
      <main class="">
        <div class="flex flex-col gap-2">
          <Balance :total="total" />
          <IncomeExpenses :income="income" :expenses="expenses" />
          <TransactionList
            :transactions="transactions"
            @transactionDeleted="handleTransactionDeleted"
          />
          <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
        </div>
      </main>
    </div>
  </div>
</template>
