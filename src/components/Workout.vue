<template>
  <div id="exerciseTracker">
    <h3>Track your Exercise</h3>

    <div id="sessionHistory">
      <h4>Previous Workouts</h4>
      <div class="historyGrid">
        <div v-if="workouts.length === 0">
          <h3>No sessions currently in history.</h3>
        </div>
        <ul v-for="session in workouts" :key="session.id">
          <li><strong>Date: {{ session.date }}</strong></li>
          <div class="aExercise">
            <template
              v-for="(stuff, index) in session.exersizes.filter(
                (item) => item.exType === 'aerobic'
              )"
            >
              <li :key="`exersize-${index}`"><strong>Exercise: </strong>{{ stuff.exercise }}</li>
              <li :key="`distance-${index}`"><strong>Distance: </strong>{{ stuff.distance }}  {{ stuff.distanceType }}</li>
              <li :key="`duration-${index}`">
                <strong>Duration: </strong>{{ stuff.duration }}
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
              <li :key="`exercise-${index}`"><strong>Exercise: </strong>{{ stuff.exercise }}</li>
              <li :key="`sets-${index}`"><strong>Sets: </strong>{{ stuff.sets }}</li>
              <li :key="`reps-${index}`"><strong>Reps: </strong>{{ stuff.reps }}</li>
              <li :key="`weight-${index}`">
                <strong>Weight: </strong>{{ stuff.weight }} {{ stuff.weightType }}
              </li>
            </template>
            <button @click="$emit('delete:session', session.id)" class="deleteButton">DELETE</button>
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
.deleteButton{
    font-size: 1rem;
  padding: 0.25rem 0.5rem;
  
  background-color: #0504aa;
  color: #f2f2f2;
  align-self: right;
  margin-top: 0.5rem;
  cursor: pointer;
}
button.deleteButton:hover {
    transition: 500ms;
    color: red;
}
</style>