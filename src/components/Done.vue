<template>
  <div class="done flex flex-col items-center justify-center">
    <div>
      <p>You did it!</p>
      <span
        >Completed {{ totalReps }} reps and breaths in {{ timeString }}
      </span>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { computed } from 'vue';

const props = defineProps<{
  totalReps: number;
  totalTime: number;
}>();

const timeString = computed(() => {
  const totalSeconds = props.totalTime / 1000;
  const hours = Math.floor(totalSeconds / 3600);
  const minutes = Math.floor((totalSeconds - hours * 3600) / 60);
  const seconds = Math.round(totalSeconds - hours * 3600 - minutes * 60);
  const minutesString = minutes.toString().padStart(2, '0');
  const secondsString = seconds.toString().padStart(2, '0');
  return `${minutesString}:${secondsString}`;
});
</script>
