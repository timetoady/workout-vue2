<template>
  <div id="exerciseTracker">
    <h3>Track your Exercise</h3>

    <div id="sessionHistory">
      <h4>Previous Workouts</h4>
      <div class="historyGrid">
        <ul v-for="session in workouts" :key="session.id">
          <li>Date: {{ session.date }}</li>
          <div class="aExercise">
            <template
              v-for="(stuff, index) in session.exersizes.filter(
                (item) => item.exType === 'aerobic'
              )"
            >
              <li :key="`exersize-${index}`">Exercise: {{ stuff.exercise }}</li>
              <li :key="`distance-${index}`">Distance: {{ stuff.distance }}</li>
              <li :key="`duration-${index}`">
                Duration: {{ stuff.duration }} {{ stuff.distanceType }}
              </li>
            </template>
          </div>

          <div class="aExercise">
            <template
              v-for="(stuff, index) in session.exersizes.filter(
                (item) => item.exType === 'anaerobic'
              )"
              class="aExercise"
            >
              <li :key="`exercise-${index}`">Exercise: {{ stuff.exercise }}</li>
              <li :key="`sets-${index}`">Sets: {{ stuff.sets }}</li>
              <li :key="`reps-${index}`">Reps: {{ stuff.reps }}</li>
              <li :key="`weight-${index}`">
                Weight: {{ stuff.weight }} {{ stuff.weightType }}
              </li>
            </template>
          </div>
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
  methods: {
    getAnaerobic: function (exercise) {
      console.log("Exercises", exercise);
      const details = exercise.filter(
        (theExercise) => theExercise.exType === "anaerobic"
      );
      console.log("Details", details);
    },
    getAerobic: function (exercise) {
      console.log("Exercises", exercise);
      console.log(exercise[1].exType);
      const details = exercise.filter(
        (theExercise) => theExercise.exType === "aerobic"
      );
      console.log("Details", details);
    },
  },
};
</script>

<style scoped>
#sessionHistory li {
  list-style: none;
}
#exerciseTracker h3 {
  margin-top: 0;
}
.historyGrid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 20px;
  text-align: left;
  border: 2px solid black;
  margin: 0.5rem auto;
  max-width: 1200px;
}
div.historyGrid > ul:nth-of-type(odd) {
    background: #eee;
}

div.historyGrid ul{
  margin: 0;
  padding: 1rem;
}
.aExercise {
  padding: 0.25rem;
}
</style>