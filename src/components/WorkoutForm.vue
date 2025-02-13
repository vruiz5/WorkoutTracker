<script setup>
import { ref, defineEmits, defineProps, watch } from 'vue';

const props = defineProps({
  editableWorkout: Object
});

const exercise = ref('');
const duration = ref('');
const calories = ref('');
const heartRate = ref('');
const reps = ref('');
const sets = ref('');
const isEditing = ref(false);

const emit = defineEmits(['workoutSubmitted']);

watch(() => props.editableWorkout, (newWorkout) => {
  if (newWorkout) {
    exercise.value = newWorkout.exercise;
    duration.value = newWorkout.duration;
    calories.value = newWorkout.calories;
    heartRate.value = newWorkout.heartRate;
    reps.value = newWorkout.reps;
    sets.value = newWorkout.sets;
    isEditing.value = true;
  }
}, { deep: true });

const onSubmit = () => {
  if (!exercise.value || !duration.value || !calories.value || !heartRate.value) return;

  const workoutData = {
    id: isEditing.value ? props.editableWorkout.id : Date.now(),
    exercise: exercise.value,
    duration: parseInt(duration.value),
    calories: parseInt(calories.value),
    heartRate: parseInt(heartRate.value),
    reps: parseInt(reps.value) || 0,
    sets: parseInt(sets.value) || 0,
  };

  emit('workoutSubmitted', workoutData);
  resetForm();
};

const resetForm = () => {
  exercise.value = '';
  duration.value = '';
  calories.value = '';
  heartRate.value = '';
  reps.value = '';
  sets.value = '';
  isEditing.value = false;
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
    <button type="submit">{{ isEditing ? 'Update Workout' : 'Add Workout' }}</button>
  </form>
</template>
