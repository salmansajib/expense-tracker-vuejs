<script setup>
const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <div
    class="bg-zinc-950 rounded-md flex gap-2 flex-col items-center justify-center p-3"
  >
    <h4 class="font-medium text-xl uppercase">Your Balance</h4>
    <h1 id="balance" class="font-medium text-5xl text-blue-500">
      ${{ total }}
    </h1>
  </div>
</template>
