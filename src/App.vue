<template>
  <div id="app">
    <h1>Workout Appens</h1>
    <workout :workouts="sessions" />
  </div>
</template>

<script>
import Workout from "./components/Workout.vue";

export default {
  name: "App",
  components: {
    Workout,
  },
  data() {
    return {
      sessions: [
        {
          id: 1,
          date: "Jan 26 2021",
          exersizes: [
            {
              exId: 1,
              exType: "aerobic",
              exercise: "Jogging",
              distance: 1.2,
              duration: "1:23",
              distanceType: "mi",
            },
            {
              exId: 2,
              exType: "anaerobic",
              exercise: "Lunges",
              sets: 4,
              reps: 15,
              weight: "5, 10, 5, 10",
              weightType: "lb",
            },
          ],
        },
        {
          id: 2,
          date: "Jan 27 2021",
          exercises: [
            {
              exId: 3,
              exType: "aerobic",
              exercise: "Swimming",
              distance: 3,
              distanceType: "kl",
              duration: "0:45",
            },
          {
            exId: 4,
              exType: "anaerobic",
              exercise: "Pushups",
              sets: 3,
              reps: 20,
              weight: "0, 0, 2",
              weightType: "lb",
            },
          ],
        },
                {
          id: 3,
          date: "Feb 15 2021",
          exercises: [
            {
              exId: 6,
              exType: "aerobic",
              exercise: "Swimming",
              distance: 3.2,
              distanceType: "kl",
              duration: "1:00",
            },
          {
            exId: 5,
              exType: "anaerobic",
              exercise: "Pushups",
              sets: 3,
              reps: 20,
              weight: "0, 0, 2",
              weightType: "lb",
            },
          ],
        },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}
</style>
