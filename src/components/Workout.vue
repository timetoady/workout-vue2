<template>
  <div id="exerciseTracker">
    <h3>Track your Exercise</h3>

    <div id="sessionHistory">
      <h4>Previous Workouts</h4>
      <div class="historyGrid">
        <ul v-for="session in workouts" :key="session.id">
          <li>Date: {{ session.date }}</li>
          <ul v-for="(exercise, index) in session.exersizes"
            class="aExercise"
            :key="`exercise${index}`">
            <li>Exercise: {{ exercise.exercise }}</li>
            <div v-if="exercise.exType === 'anaerobic'">
              <li>Distance: {{ exercise.distance }}</li>
              <li>
                Duration: {{ exercise.duration }} {{ exercise.distanceType }}
              </li>
            </div>
            <div v-if="exercise.exType === 'aerobic'">
              <li>Sets: {{ exercise.sets }}</li>
              <li>Reps: {{ exercise.reps }}</li>
              <li>Weight: {{ exercise.weight }} {{ exercise.weightType }}</li>
            </div>
          </ul>
        </ul>
      </div>
      <div></div>
    </div>
  </div>
</template>

<script>

export default {
    
  name: "Workout",
  props: {
    workouts: Array,
  },
};
</script>

<style scoped>
#sessionHistory li {
  list-style: none;
}
.historyGrid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 20px;
  text-align: left;
  border: 2px solid black;
  padding: 0.5rem;
  margin: 0.5rem auto;
  max-width: 1200px;
}
.addButtons {
  display: flex;
  justify-content: space-around;
}
.weightDiv {
  display: flex;
}
#theWeight {
  padding: 0.5rem;
}
.aExercise {
  padding: 0.5rem;
}
</style>