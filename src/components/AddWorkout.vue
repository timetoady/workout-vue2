<template>
   <div id="addNew">
      <div class="addButtons">
        <button>Aerobic +</button>
        <button>Anaerobic +</button>
      </div>

      <div id="addAerobic">
        <form action="" class="small-container">
          <h3>Anaerobic</h3>
          <label> Exercise<input type="text" name="exerciseAn" /> </label>
          <label> # Sets<input type="number" name="sets" /> </label>
          <label> # Reps<input type="number" name="reps" /> </label>
          <div class="weightDiv">
            <div>
              <label> Weight<input type="number" name="weight" /> </label>
            </div>
            <div>
              <select name="weightType" id="theWeight">
                <option value="kg">KG</option>
                <option value="lb">LB</option>
              </select>
            </div>
          </div>
        </form>
      </div>

      <div id="addAnaerobic">
        <form action="" class="small-container">
          <h3>Aerobic</h3>
          <label> Exercise<input type="text" name="exerciseAe" /> </label>
          <label> Distance<input type="number" name="distance" /> </label>
          <label>
            Duration<input type="time" name="duration1" /> to
            <input type="time" name="duration2"
          /></label>
          <div class="distanceDiv">
            <div>
              <select name="distanceType" id="theDistance">
                <option value="mi">MI</option>
                <option value="kl">KL</option>
              </select>
            </div>
          </div>
        </form>
      </div>
    </div>
</template>

<script>
export default {

}
</script>

<style>

</style>