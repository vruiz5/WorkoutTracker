<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  workouts: Array,
});

const emit = defineEmits(['deleteWorkout', 'editWorkout']);
</script>

<template>
  <h3>Workout History</h3>
  <ul>
    <li v-for="workout in workouts" :key="workout.id">
      <div>
        <strong>{{ workout.exercise }}</strong> - {{ workout.duration }} min, {{ workout.calories }} cal
        <br />
        Heart Rate: {{ workout.heartRate }} BPM | Reps: {{ workout.reps }} | Sets: {{ workout.sets }}
      </div>
      <button @click="emit('editWorkout', workout)">Edit</button>
      <button @click="emit('deleteWorkout', workout.id)">Delete</button>
    </li>
  </ul>
</template>
