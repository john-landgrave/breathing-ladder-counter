<template>
  <div class="self-center h-full">
    <form class="flex flex-col h-full" @submit.prevent="$emit('continue')">
      <div class="flex-1 flex flex-col items-center justify-center">
        <p class="mb-4">How many reps will you peak at tonight?</p>
        <input
          class="
            bg-transparent
            border-none
            text-3xl text-green-400
            outline-none
            text-center
            mb-8
          "
          placeholder="0"
          type="text"
          v-model.number="peakRepNumber"
        />
      </div>
      <button
        class="
          px-5
          py-2
          text-center
          rounded-xl
          text-white
          bg-green-500
          self-center
          bigButton
        "
      >
        Continue
      </button>
    </form>
  </div>
</template>

<script setup lang="ts">
const [peakRepNumber] = defineModel('peakRepNumber');
defineEmits(['continue']);
</script>
