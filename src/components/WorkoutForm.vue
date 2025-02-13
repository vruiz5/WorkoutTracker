<script setup>
import { ref, defineEmits } from 'vue'

const exercise = ref('')
const duration = ref('')
const calories = ref('')
const heartRate = ref('')
const reps = ref('')
const sets = ref('')

const emit = defineEmits(['workoutSubmitted']);

const onSubmit = () => {
  if (!exercise.value || !duration.value || !calories.value || !heartRate.value) return

  emit('workoutSubmitted', {
    exercise: exercise.value,
    duration: parseInt(duration.value),
    calories: parseInt(calories.value),
    heartRate: parseInt(heartRate.value),
    reps: parseInt(reps.value) || 0,
    sets: parseInt(sets.value) || 0,
  });

  exercise.value = ''
  duration.value = ''
  calories.value = ''
  heartRate.value = ''
  reps.value = ''
  sets.value = ''
};
</script>

<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="exercise" placeholder="Exercise Name" />
    <input type="number" v-model="duration" placeholder="Duration (minutes)" />
    <input type="number" v-model="calories" placeholder="Calories Burned" />
    <input type="number" v-model="heartRate" placeholder="Max Heart Rate" />
    <input type="number" v-model="reps" placeholder="Reps (Optional)" />
    <input type="number" v-model="sets" placeholder="Sets (Optional)" />
    <button type="submit">Add Workout</button>
  </form>
</template>
