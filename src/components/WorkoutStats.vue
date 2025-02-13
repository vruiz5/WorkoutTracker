<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  totalTime: Number,
  totalCalories: Number,
  mostCalories: Number,
  leastCalories: Number,
});
</script>

<template>
  <div class="stats-container">
    <h4>Total Workout Time: {{ totalTime }} minutes</h4>
    <h4>Total Calories Burned: {{ totalCalories }}</h4>
    <h4>Most Calories Burned in a Workout: {{ mostCalories }}</h4>
    <h4>Least Calories Burned in a Workout: {{ leastCalories }}</h4>
  </div>
</template>
