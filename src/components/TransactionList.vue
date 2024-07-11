<script setup>
const emit = defineEmits(["transactionDeleted"]);

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const deleteTransaction = (id) => {
  emit("transactionDeleted", id);
};
</script>

<template>
  <div class="bg-zinc-950 p-3 rounded-md">
    <h3 class="text-center font-semibold text-2xl mb-3">History</h3>
    <ul id="list" class="list flex flex-col gap-2">
      <li
        v-for="transaction in transactions"
        :key="transaction.id"
        :class="
          transaction.amount < 0
            ? 'minus flex items-center justify-between p-2 bg-red-700 rounded'
            : 'minus flex items-center justify-between p-2 bg-green-700 rounded'
        "
      >
        {{ transaction.text }}
        <div>
          <span class="">${{ transaction.amount }}</span
          ><button
            @click="deleteTransaction(transaction.id)"
            class="cursor-pointer ml-5"
          >
            <i class="pi pi-trash hover:text-white"></i>
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>
