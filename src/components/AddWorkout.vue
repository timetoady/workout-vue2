<template>
  <div id="addNew">
    <div class="addButtons">
      <button id="aeroAdd" @click="toggleActive(1)">Aerobic +</button>
      <button id="anaeroAdd" @click="toggleActive(0)">Anaerobic +</button>
    </div>

    <div id="addAnaerobic" v-if="item.isAnaero === true">
      <h3>Anaerobic</h3>
      <form @submit.prevent="addExer" class="small-container">
        <label>
          Exercise
          <input
            placeholder="Pushups"
            type="text"
            name="exercise"
            v-model="item.exerciseAn"
          />
        </label>
          <label>
            Date 
          <input type="date" name="date" v-model="item.date">
        </label>
        <label>
          # Sets
          <input
            type="number"
            name="sets"
            v-model="item.sets"
            max="100"
            min="0"
          />
        </label>
        <label>
          # Reps <input type="number" name="reps" v-model="item.reps" min="0" />
        </label>
        <div class="weightDiv" v-if="item.sets > 0">
          <label>
            Weight
            <input
              type="text"
              name="weight"
              v-model="item.weight"
              placeholder="10, 15"
                 />
            <select name="weightType" id="theWeight" v-model="item.weightType">
              <option value="kg">KG</option>
              <option value="lb">LB</option>
            </select>
            <div class="distanceDiv"></div>
            <div></div>
            <div class="distanceDiv">
              <button class="addButton">ADD</button>
            </div>
          </label>
        </div>
      </form>
    </div>

    <div id="addAerobic" v-if="item.isAero === true">
      <h3>Aerobic</h3>
      <form @submit.prevent="addExer" class="small-container">
        <label
          >Exercise
          <input
            placeholder="Jogging"
            type="text"
            name="exercise"
            v-model="item.exerciseAe"
          />
        </label>
        <label>Date 
          <input type="date" name="date" v-model="item.date">
        </label>
        <label
          >Distance
          <input
            type="number"
            name="distance"
            v-model="item.distance"
            max="100"
            min="0"
          />
          <select
            name="distanceType"
            id="theDistance"
            v-model="item.distanceType"
          >
            <option value="mi">MI</option>
            <option value="kl">KL</option>
          </select>
        </label>
        <label>
          Duration
          <input type="time" name="duration1" v-model="item.duration1" /> to
          <input type="time" name="duration2" v-model="item.duration2" />
        </label>
        <div class="distanceDiv"></div>
        <div></div>
        <div class="distanceDiv">
          <button class="addButton">ADD</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "add-exercise",
  data() {
    return {
      item: {
        date: new Date().toISOString().split('T')[0],
        exerciseAn: "",
        exerciseAe: "",
        sets: 2,
        reps: 1,
        weight: "",
        weightType: "lb",
        distance: 0,
        duration1: "",
        duration2: "",
        distanceType: "mi",
        isAero: false,
        isAnaero: false,
        exType: "",
        added: false,
      },
    };
  },
  methods: {
    toggleActive(type) {
      if (type === 0) {
        this.item.isAero = false;
        this.item.isAnaero = true;
        this.item.exType= 'anaerobic'
      } else {
        this.item.isAero = true;
        this.item.isAnaero = false;
        this.item.exType= 'aerobic'
      }
    },
    addExer() {
      this.item.added = true;
      this.$emit('add:item', this.item)
    }
  },
};
</script>

<style>
.small-container {
  max-width: 50rem;
  margin: 0 auto;
  display: grid;
  gap: 20px;
  grid-template-columns: 1fr 1fr;
  
}
div#addAerobic,
div#addAnaerobic {
  max-width: 900px;
  margin: 1rem auto;
  border: 2px ridge;
  padding: 0.5rem;
}
.addButtons {
  display: flex;
  justify-content: space-around;
}

.addButtons button {
  font-size: 1.5rem;
  padding: 0.25rem 0.5rem;
  background-color: #0504aa;
  color: #f2f2f2;
  border-radius: 6px;
  cursor: pointer;
}
.addButton {
  font-size: 1rem;
  padding: 0.25rem 0.5rem;
  max-width: 4rem;
  background-color: #0504aa;
  color: #f2f2f2;
  align-self: right;
  margin-top: 0.5rem;
  cursor: pointer;
  
}

.distanceDiv {
  display: flex;
  justify-content: space-between;
}
/* .weightDiv {
  display: flex;
} */
label.weightDiv {
  display: flex;
}
.aExercise {
  padding: 0.5rem;
}
input {
  margin: 0;
  font-size: 1.2rem;
}
select {
  margin: 0;
  font-size: 1.2rem;
}
.highlighted {
  border: 3px green solid;
}
</style>