<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const text = ref("");
const amount = ref("");

const emit = defineEmits(["transactionSubmitted"]);

const toast = useToast();

const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error("Both field must be filled");
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit("transactionSubmitted", transactionData);

  text.value = "";
  amount.value = "";
};
</script>

<template>
  <div class="bg-zinc-950 p-3 rounded-md">
    <h3 class="text-center font-semibold text-2xl mb-3">Add new transaction</h3>
    <form @submit.prevent="onSubmit" class="flex flex-col gap-2">
      <div class="flex flex-col gap-2">
        <label for="text">Transation Name</label>
        <input
          class="p-2 rounded bg-gray-200 placeholder:text-gray-500 text-gray-950"
          type="text"
          id="text"
          v-model="text"
          placeholder="Enter text..."
        />
      </div>
      <div class="flex flex-col gap-2">
        <label for="amount"
          >Amount <br />
          (negative - expense, positive - income)</label
        >
        <input
          class="p-2 rounded bg-gray-200 placeholder:text-gray-500 text-gray-800"
          type="text"
          id="amount"
          v-model="amount"
          placeholder="Enter amount..."
        />
      </div>
      <button
        class="bg-purple-600 hover:bg-purple-700 p-2 rounded transition-colors"
      >
        Add Transaction
      </button>
    </form>
  </div>
</template>
