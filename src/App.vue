<script setup>
import { ref, computed, onMounted } from 'vue';
import Header from './components/Header.vue';
import WorkoutForm from './components/WorkoutForm.vue';
import WorkoutList from './components/WorkoutList.vue';
import WorkoutStats from './components/WorkoutStats.vue';

const workouts = ref([]);
const editableWorkout = ref(null);

const totalTime = computed(() => workouts.value.reduce((acc, workout) => acc + workout.duration, 0));
const totalCalories = computed(() => workouts.value.reduce((acc, workout) => acc + workout.calories, 0));
const mostCalories = computed(() => {
  if (workouts.value.length === 0) return 0;
  return Math.max(...workouts.value.map(w => w.calories));
})
const leastCalories = computed(() => {
  if (workouts.value.length === 0) return 0;
  return Math.min(...workouts.value.map(w => w.calories));
})

const addWorkout = (workout) => {
  if (workouts.value.some(w => w.id === workout.id)) {
    workouts.value = workouts.value.map(w => (w.id === workout.id ? workout : w));
  } else {
    workouts.value.push(workout);
  }
  saveToLocalStorage();
};

const deleteWorkout = (id) => {
  workouts.value = workouts.value.filter(workout => workout.id !== id);
  saveToLocalStorage();
};

const editWorkout = (workout) => {
  editableWorkout.value = { ...workout };
};

const saveToLocalStorage = () => {
  localStorage.setItem('workouts', JSON.stringify(workouts.value));
};

onMounted(() => {
  const savedWorkouts = JSON.parse(localStorage.getItem('workouts'));
  if (savedWorkouts) {
    workouts.value = savedWorkouts;
  }
});
</script>

<template>
  <Header />
  <WorkoutStats :totalTime="totalTime" :totalCalories="totalCalories" :mostCalories="mostCalories" :leastCalories="leastCalories" />
  <WorkoutForm @workoutSubmitted="addWorkout" :editableWorkout="editableWorkout" />
  <WorkoutList :workouts="workouts" @deleteWorkout="deleteWorkout" @editWorkout="editWorkout" />
</template>

<style scoped>
@import './style.css';
</style>
