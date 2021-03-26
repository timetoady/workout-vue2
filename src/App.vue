<template>
  <div id="app">
    <h1 class="title">Workout Appens</h1>
    <workout :workouts="sessions" />
    <add-workout @add:item="addItem"/>
      <div id="currentSession">
      
       <div id="sessionDisplay" v-if="adding === true && currentSess.id">
         <h3>Current session:</h3> 
         <h4>Date: {{currentSess.date}}</h4>
         <div class="exerciseList">

            <template v-for="(oneExer, index) in currentSess.exersizes.filter(
                (item) => item.exType === 'aerobic')">
                <div class="exerSet" :key="`div-${index}`">
              <h5 :key="`exersize-${index}`">Exercise: {{ oneExer.exercise }}</h5>
           <h5 :key="`distance-${index}`">Distance: {{ oneExer.distance }} {{oneExer.distanceType}}</h5>
           <h5 :key="`duration-${index}`">Duration: {{ oneExer.duration }}</h5>
                </div>

         </template>
        

         
            <template  v-for="(oneExer, index) in currentSess.exersizes.filter(
                (item) => item.exType === 'anaerobic')">
                <div class="exerSet" :key="`div-${index}`">
           <h5 :key="`exersize-${index}`">Exercise: {{ oneExer.exercise }}</h5>
           <h5 :key="`set-${index}`">Sets: {{ oneExer.sets }}</h5>
           <h5 :key="`reps-${index}`">Reps: {{ oneExer.reps }}</h5>
           <h5 :key="`weight-${index}`">Weight: {{ oneExer.weight }} {{oneExer.weightType.toUpperCase()}}</h5>
           </div>
         </template>
         

         </div>
        <button @click="completeSess" class="completeButton">Complete</button>
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
              duration: "1.36 hours",
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
              duration: "45 minutes",
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
              duration: "1.00 hours",
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
      currentSess: {},
      adding: false,
    };
  },
  methods: {
    addItem(item){
      console.log("Item to add", item)
      console.log("Current session: ", this.currentSess)
      this.adding = item.added
      if (Object.keys(this.currentSess).length === 0 && this.currentSess.constructor === Object) {
      console.log("current session empty, adding id and date")  
      const lastId = this.sessions.length > 0 ? this.sessions[this.sessions.length -1].id : 0;
      this.currentSess.id = (lastId + 1)
      this.currentSess.exersizes = []
      }
      if (item.isAnaero === true) {
        this.currentSess.date = item.date;
        let exerObject = {}
        exerObject.exType = "anaerobic"
        exerObject.exercise = item.exerciseAn
        exerObject.sets = item.sets
        exerObject.reps = item.reps
        exerObject.weight = item.weight
        exerObject.weightType = item.weightType
        exerObject.exType = item.exType
        this.currentSess.exersizes = [...this.currentSess.exersizes, exerObject]
      } else {
        this.currentSess.date = item.date;
        let exerObject = {}
        exerObject.exType = "aerobic"
        exerObject.exercise = item.exerciseAe
        exerObject.distance = item.distance
        let calcDuration = this.getTimeDiff(item.duration1, item.duration2)
        exerObject.duration = calcDuration
        exerObject.distanceType = item.distanceType
        exerObject.exType = item.exType
        console.log("Current sess before add", this.currentSess)
        this.currentSess.exersizes = [...this.currentSess.exersizes, exerObject]
      }
      console.log("Session exercizes after add: ", this.currentSess.exersizes)
      this.currentSess = {...this.currentSess}
  
    },
    getTimeDiff(time1, time2) {
      let hours1 = time1.split(':')[0]
      let hours2 = time2.split(':')[0]
      let minutes1 = time1.split(':')[1]
      let minutes2 = time2.split(':')[1]
      let timeInMinutes1 = (parseInt(hours1) * 60) + parseInt(minutes1)
      let timeInMinutes2 = (parseInt(hours2) * 60) + parseInt(minutes2)
      let theDiff = timeInMinutes2 - timeInMinutes1
      const diffInHours = (theDiff / 60)
      if (diffInHours < 1) {
        return `${theDiff.toFixed(2)} minutes`
      } else{
        return `${diffInHours.toFixed(2)} hours`
      }
      
    },
    completeSess() {
      console.log("Sess before change", this.sessions)
      this.sessions = [...this.sessions, this.currentSess]
      console.log("Sess after change", this.sessions)
      this.currentSess = {}
      this.adding = false;
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
.exerciseList{
  display: flex;
  justify-content: space-evenly;
}
.oneExercise{
  display: flex;
  
}
.exerSet{
  padding: 1rem;
}
</style>
