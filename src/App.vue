<script setup lang="ts">
import { ref, computed, type Ref } from 'vue';
import Setup from './components/Setup.vue';
import Reps from './components/Reps.vue';
import Breaths from './components/Breaths.vue';
import Done from './components/Done.vue';

type WhatToShow = 'setup'|'reps'|'breaths'|'done';
type NumberDirection = 'up'|'down';

const currentNumberDirection: Ref<NumberDirection> = ref('up');
const numberOfReps = ref();
const currentRepCount = ref(0);
const totalReps = ref(0);
const currentStep: Ref<WhatToShow> = ref('setup');
const tick: Ref<number|undefined> = ref(undefined);
const tock: Ref<number|undefined> = ref(undefined);
let wakeLockSentinel: WakeLockSentinel|undefined = undefined;

const finishSetup = async () => {
  currentRepCount.value = Math.min(numberOfReps.value, 1);
  tick.value = Date.now();
  try {
    wakeLockSentinel = await navigator.wakeLock.request("screen");
  } catch(e) {}
  currentStep.value = 'reps';
};

const completeReps = () => {
  currentStep.value = 'breaths';
  totalReps.value += currentRepCount.value;
};

const completeBreaths = () => {
  currentStep.value = 'reps';
  if (currentRepCount.value === numberOfReps.value) {
    currentNumberDirection.value = 'down';
  }

  if (currentNumberDirection.value === 'up') {
    currentRepCount.value++;
  } else {
    if (currentRepCount.value === 1) {
      tock.value = Date.now();
      currentStep.value = 'done';
      wakeLockSentinel?.release();
      return;
    }

    currentRepCount.value--;
  }
}

const totalTime = computed(() => {
  if (typeof tick.value !== 'undefined' && typeof tock.value !== 'undefined') {
    return tock.value - tick.value;
  }
  return 0;
})
</script>

<template>
  <Setup
    v-if="currentStep === 'setup'"
    v-model:peakRepNumber.number="numberOfReps"
    @continue="finishSetup"
  ></Setup>
  <Reps
    :repCount="currentRepCount"
    v-if="currentStep === 'reps'"
    @complete="completeReps"
  ></Reps>
  <Breaths
    :breathCount="currentRepCount"
    v-if="currentStep === 'breaths'"
    @complete="completeBreaths"
  ></Breaths>
  <Done
    v-if="currentStep === 'done'"
    :totalReps="totalReps"
    :totalTime="totalTime"
  ></Done>
</template>

<style scoped></style>
