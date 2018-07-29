<template>

  <div class='wrapper'>
  
   <div class="title">Vue.js Calorie Counter</div> 
  <div class="header">
    <p class='des'>DESCRIPTION</p>
    <p >CALORIES</p>
    <p>FAT</p>
    <p>CARBS</p>
    <p>PROTEINS</p>
  </div>


  <div class="entry" v-bind:key="entry.id" v-for="entry in entries">
    <input class='description' type="text" v-model="entry.description" v-on:keyup.enter="saveEntry">
    <input class='mini'  type="number" v-model="entry.calories"  v-on:keyup.enter="saveEntry">
    <input class='mini'  type="number" v-model="entry.fat" v-on:keyup.enter="saveEntry">
    <input  class='mini' type="number" v-model="entry.carbs"  v-on:keyup.enter="saveEntry">
    <input  class='mini' type="number" v-model="entry.protein" v-on:keyup.enter="saveEntry">
    <button class="delete" v-on:click="removeEntry($index)">
      x
    </button>
  </div>


  <div class="totals">
    <p>Totals: </p>
    <p>{{ totalCalories }}</p>
    <p>{{ totalFat }}</p>
    <p>{{ totalCarbs }}</p>
    <p>{{ totalProtein }}</p>
  </div>


  <div class="new">
    <input  type="text" class='des' v-model="newDescription" v-on:keyup.enter="addEntry" placeholder="Description">
    <input type="number" class='mini' v-model="newCalories" v-on:keyup.enter="addEntry" placeholder="Calories">
    <input type="number" class='mini' v-model="newFat" v-on:keyup.enter="addEntry" placeholder="Fat">
    <input type="number" class='mini' v-model="newCarbs" v-on:keyup.enter="addEntry"  placeholder="Carbs">
    <input type="number" class='mini' v-model="newProtein" v-on:keyup.enter="addEntry"  placeholder="Protein">
    <button class="add" v-on:click="addEntry()">+</button>
  </div>


</div>
   
</template>






<script>
export default {
  name: 'calMeter',
  props: {
    msg: String
  },
  data() {
    return{
          newDescription: '',
          newCalories: '',
          newFat: '',
          newCarbs: '',
          newProtein: '',
          totalCalories: '',
          totalFat: '',
          totalCarbs: '',
          totalProtein: '',
          entries: [
                { id: 1, description:'This is an item', calories: 223, fat: 12, carbs: 30, protein: 10 },
                { id: 2, description:'This is also an item', calories: 50, fat: 1, carbs: 10, protein: 1 },
                { id: 3, description:'Hey, me, too!', calories: 175, fat: 3, carbs: 15, protein: 8 }
          ]
        }
    },
  
  methods: {

    addEntry: function () {
      var description = this.newDescription.trim()
      var calories = parseInt(this.newCalories.trim()) || 0
      var fat = parseInt(this.newFat.trim()) || 0
      var carbs = parseInt(this.newCarbs.trim()) || 0
      var protein = parseInt(this.newProtein.trim()) || 0
      if (description && calories) {
        this.entries.push(
          { description: description, 
            calories: calories, 
            fat: fat, 
            carbs: carbs, 
            protein: protein 
          }
        )

        this.newDescription = ''
        this.newCalories = ''
        this.newFat = ''
        this.newCarbs = ''
        this.newProtein = ''
      
        calculateTotals(this)
      } else {
        alert("pls fill out all fields")
      }
    },

    removeEntry: function (index) {
      this.entries.splice(index, 1)
      calculateTotals(this)
    },

    saveEntry: function() {
      calculateTotals(this)
    }
  }
}

function calculateTotals(app) {
  app.totalCalories = parseTotals(app.entries, 'calories')
  app.totalFat = parseTotals(app.entries, 'fat')
  app.totalCarbs = parseTotals(app.entries, 'carbs')
  app.totalProtein = parseTotals(app.entries, 'protein')
}

</script>





















<style lang="scss">




.wrapper {
    color: #444;
    background: white;
    font-family: 'Roboto', sans-serif;
    border: 1px solid lightgray;
    border-radius: 10px;

.title {
  padding: 20px;
  margin-bottom: 10px;
  color: lightgray;
  font-size: 5vh;
  background:#009688;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  width: 700px;
  position: relative;
  text-align: center;
  overflow:hidden;
}
.header {
  display: flex;
  justify-content: flex-start;
  margin-left: 10px;
  margin-bottom: 10px;



  p{
    margin-right: 6vw;
    font-size: 2vh;
  }

  .des{
    margin-right: 110px;
  }

}
.entry {
  margin-left: 10px;
  color: #40464f;
  .mini {
    width: 6vw;
    color: #40464f;
    margin-right: 3vw;
  }
  .description {
    margin-right: 40px;
    color: #40464f;
  }

}

 .new {
  font-size: 0;
  position: relative;
  padding-top: 30px;
  padding-left: 20px;
  padding-bottom: 20px;

    .mini {
    width: 6vw;
    margin-right: 3vw;
  }

   .des {
     margin-right: 15px;
   }
}
.entry + .entry {
  margin-top: 2.25%;
}
.totals {
  color: 40464f;
  margin-top: 20px;
  width: 588px;
  padding-left: 149px;
  background: lightgray;
  border: 1px solid darkgray;


 
}

input {
  background: transparent;
  display: inline;
  border: none;
  border-bottom: black;
  padding: .15rem;
  color: black;
 
}

.add {
  margin-left: 92%;
  margin-top: -15px;
  background:#009688;
  font-size: 3rem;
  position: absolute;
  display: block;
  width: 4rem;
  height: 4rem;
  border-radius: 50%;
  border: transparent;
  color: white;
}
.delete {
    position: absolute;
  display: block;
  border: transparent;
  background: transparent;
  font-size: 20px;
  color: gray;  
  margin-left: 50%;
  margin-top: -25px;
}
}
</style>
