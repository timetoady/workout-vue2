<template>
  <div id="exerciseTracker">
    <h3>Track your Exercise</h3>

    <div id="sessionHistory">
      <h4>Workout History</h4>
      <div class="nothingHere" v-if="workouts.length === 0">
        <p>No workout sessions currently in history.</p>
      </div>
      <div class="historyGrid">
        <ul v-for="session in workouts" :key="session.id">
          <li>
            <strong>Date: {{ session.date }}</strong>
          </li>
          <div class="aExercise">
            <template
              v-for="(stuff, index) in session.exersizes.filter(
                (item) => item.exType === 'aerobic'
              )"
            >
              <li class="exerStart" :key="`exersize-${index}`">
                <strong>Exercise: </strong>{{ stuff.exercise }}
              </li>
              <li :key="`distance-${index}`">
                <strong>Distance: </strong>{{ stuff.distance }}
                {{ stuff.distanceType }}
              </li>
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
              <li class="exerStart" :key="`exercise-${index}`">
                <strong>Exercise: </strong>{{ stuff.exercise }}
              </li>
              <li :key="`sets-${index}`">
                <strong>Sets: </strong>{{ stuff.sets }}
              </li>
              <li :key="`reps-${index}`">
                <strong>Reps: </strong>{{ stuff.reps }}
              </li>
              <li :key="`weight-${index}`">
                <strong>Weight: </strong>{{ stuff.weight }}
                {{ stuff.weightType }}
              </li>
            </template>
            <div class="editDelete">
              <button
                @click="$emit('delete:session', session.id)"
                class="deleteButton"
              >
                DELETE
              </button>
            </div>
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
  border: 10px inset;
  margin: 0.5rem auto;
  max-width: 1200px;
  padding: 20px;
}
@media screen and (max-width: 900px){
  .historyGrid {
    grid-template-columns: 1fr 1fr;
  }
}
@media screen and (max-width: 700px){
  .historyGrid {
    grid-template-columns: 1fr;
  }
}
div.historyGrid > ul:nth-of-type(odd) {
  background: #f3f3f3;
  border: 2px solid rgba(0, 0, 0, 0.712);
  box-shadow: 1px 1px 5px black;
  border-radius: 6px;
}
div.historyGrid > ul:nth-of-type(even) {
  background: rgb(63, 114, 251);
  color: white;
  text-shadow: 1px 1px 2px black;
  border: 2px solid rgba(0, 0, 0, 0.685);
  border-radius: 6px;
  box-shadow: 1px 1px 5px black;
}

div.historyGrid ul {
  margin: 0;
  padding: 1rem;
}
.nothingHere {
  margin: 0;
  padding: 1rem;
}
.aExercise {
  padding: 0.25rem;
}
.exerStart{
  padding-top: 10px;
}
.deleteButton {
  font-size: 1rem;
  padding: 0.25rem 0.5rem;

  background-color: #0504aa;
  color: #f2f2f2;
  align-self: right;
  margin-top: 0.5rem;
  cursor: pointer;
  border-radius: 3px;
}
button.deleteButton:hover {
  transition: 500ms;
  color: red;
}
.editDelete {
  display: flex;
  justify-content: space-evenly;
}
</style>