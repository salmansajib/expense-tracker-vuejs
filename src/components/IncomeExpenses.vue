<script setup>
const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expenses: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <div class="inc-exp-container flex gap-2 items-center justify-center">
    <div class="bg-zinc-950 basis-full p-3 rounded-md text-center">
      <h4 class="uppercase">Income</h4>
      <p id="money-plus" class="money plus text-2xl text-green-500">
        ${{ income }}
      </p>
    </div>
    <div class="bg-zinc-950 basis-full p-3 rounded-md text-center">
      <h4 class="uppercase text-lg">Expense</h4>
      <p id="money-minus" class="money minus text-2xl text-red-500">
        ${{ expenses }}
      </p>
    </div>
  </div>
</template>
