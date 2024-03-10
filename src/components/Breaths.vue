<template>
  <div class="reps self-center h-full">
    <form class="py-4 flex flex-col h-full" @submit.prevent="$emit('complete')">
      <div class="flex-1 flex items-center justify-center">
        <span class="text-5xl text-blue-400">
          {{ breathCount }}
        </span>
      </div>
      <button
        class="
          px-5
          py-2
          text-center
          rounded-xl
          text-white
          bg-green-400
          bigButton
        "
      >
        Start Reps
      </button>
    </form>
  </div>
</template>

<script lang="ts" setup>
defineEmits(['complete']);
defineProps<{
  breathCount: number;
}>();
</script>
