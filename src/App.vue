<template>
  <div id="app">
    <h1 class="title">Workout Appens</h1>
    <workout :workouts="sessions" />
    <add-workout @add:item="addItem"/>
      <div id="currentSession">
      <h3>Current session:</h3> 
       <div id="sessionDisplay" v-if="currentSess.length > 0">
         <h4>Date: {{currentSess[0].date}}</h4>
         <div>
           <h5>Exercise: {{currentSess[0].date}}</h5>
         </div>
        <button class="completeButton">Complete</button>
       </div>



       
   </div>
  </div>
</template>

<script>
import Workout from "./components/Workout.vue";
import AddWorkout from './components/AddWorkout.vue';


export default {
  name: "App",
  components: {
    Workout,
    AddWorkout,
    
  },
  data() {
    return {
      sessions: [
        {
          id: 1,
          date: "Jan 26 2021",
          exersizes: [
            {
              
              exType: "aerobic",
              exercise: "Jogging",
              distance: 1.2,
              duration: "1:23",
              distanceType: "mi",
            },
            {
              
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
          exersizes: [
            {
              
              exType: "aerobic",
              exercise: "Swimming",
              distance: 3,
              distanceType: "kl",
              duration: "0:45",
            },
          {
            
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
          exersizes: [
            {
              
              exType: "aerobic",
              exercise: "Swimming",
              distance: 3.2,
              distanceType: "kl",
              duration: "1:00",
            },
          {
            
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
      currentSess: []
    };
  },
  methods: {
    addItem(item){
      console.log("Item to add", item)
      console.log("Current session: ", this.currentSess)
      let filteredItem = {}
      if (this.currentSess.length === 0) {
      console.log("current session empty, adding id and date")  
      const lastId = this.sessions.length > 0 ? this.sessions[this.sessions.length -1].id : 0;
      filteredItem.id = (lastId + 1)
      filteredItem.date = item.date;
      filteredItem.exersizes = []
      this.currentSess = [filteredItem]
      }
      if (item.isAnaero === true) {
        let exerObject = {}
        exerObject.exType = "anaerobic"
        exerObject.exercise = item.exerciseAn
        exerObject.sets = item.sets
        exerObject.reps = item.reps
        this.currentSess[0].exersizes = [...this.currentSess[0].exersizes, exerObject]
      } else {
        let exerObject = {}
        exerObject.exType = "aerobic"
        exerObject.exercise = item.exerciseAe
        exerObject.distance = item.distance
        let calcDuration = (parseInt(item.duration2) - parseInt(item.duration1))
        exerObject.duration = calcDuration
        console.log("Current sess before add", this.currentSess[0])
        this.currentSess[0].exersizes = [...this.currentSess[0].exersizes, exerObject]
      }
      console.log("Filtered item: ", filteredItem)
      // this.currentSess = [filteredItem]
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  max-width: 1200px;
  padding: .3rem;
  margin: 0 auto;
  color: #2c3e50;
}
.title{
  margin-bottom: 0;
  font-size: 3rem;
  font-weight: 200;
  font-family: Arial, Helvetica, sans-serif;
  text-decoration: goldenrod;
  color: #0504aa;
  text-shadow: 2px 2px 5px black;
}
.completeButton{
    font-size: 1.5rem;
  padding: 0.25rem 0.5rem;
  background-color: #0504aa;
  color: #f2f2f2;
}
</style>
