<template>
  <div class="reps self-center h-full">
    <form class="py-4 flex flex-col h-full" @submit.prevent="$emit('complete')">
      <div class="flex-1 flex items-center justify-center">
        <span class="text-5xl text-green-400">
          {{ repCount }}
        </span>
      </div>
      <button
        class="
          px-5
          py-2
          text-center
          rounded-xl
          text-white
          bg-blue-400
          bigButton
        "
      >
        Start Breathing
      </button>
    </form>
  </div>
</template>

<script lang="ts" setup>
defineEmits(['complete']);
defineProps<{
  repCount: number;
}>();
</script>
