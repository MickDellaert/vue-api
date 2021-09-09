<template>
  <div class="container">
    <div v-if="showModal">
      <RecipeModal :recipe-results-prop="recipeResults" :ingredients-prop="ingredients" @close="toggleModal"/>
    </div>
    <div class="messagecontainer">
      <div v-if="!show" class="hello">
        <!--    <img alt="food logo" src="@/assets/food-serving.png">-->
        <h1>{{ msg }}</h1>
      </div>

      <div class="search">
        <input v-model="mealQuery" placeholder="search by ingredient">
        <button @click="fetchFood">Search Food!</button>
        <h2 v-if="mealQuery !== ''">You searched for: {{ mealQuery }}</h2>
        <h3 v-if="show">Click on the thumbnail for more information</h3>
      </div>
    </div>

    <div class="error" v-if="errorMsg">
      {{ errorMsg }}
    </div>


    <div v-if="show" class="results">
      <ul class="list-container">
        <li class="card" @click="getRecipe(meal); toggleModal()" v-for="meal in mealResults.meals" :key="meal.idMeal">
          <h4>{{ meal.strMeal }}</h4>
          <img class="foodthumb" :src="meal.strMealThumb">
        </li>
      </ul>
    </div>
  </div>

</template>

<script>
import RecipeModal from "./RecipeModal";

export default {
  name: 'HelloWorld',
  components: {RecipeModal},

  data() {
    return {
      mealQuery: "",
      msg: "Search for a recipe",
      mealResults: [],
      errorMsg: "",
      recipeResults: [],
      showModal: false,
      ingredients: [],
      show: false,
    }
  },

  // Load API response on page load (disabled for now)
  // mounted() {
  //   this.fetchFood()
  // },

  methods: {

    async fetchFood() {
      if (this.mealQuery !== "") {

        const response = await fetch(`https://www.themealdb.com/api/json/v1/1/filter.php?i=${this.mealQuery}`);
        const results = await response.json();

        if (results.meals == null) {

          this.errorMsg = `Unfortunately, we couldn't find any recipe with ${this.mealQuery}, something else you fancy?`;
          this.show = false;

          // console.log('error')
          // console.log(results.meals)

        } else {
          this.mealResults = results;
          // console.log(results);
          this.errorMsg = "";
          this.show = true;
        }
      }
    },

    async getRecipe(meal) {
      const response = await fetch(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${meal.idMeal}`)

      const results = await response.json();
      this.recipeResults = results;
      console.log(this.recipeResults.meals[0].strMeasure1);

      this.meal = results.meals[0]
      this.ingredients.splice(0);

      for (let index = 0; index < 20; index++) {
        let num = index + 1
        let ingredientName = this.meal[`strIngredient${num}`]
        let amount = this.meal[`strMeasure${num}`]

        const item = {
          id: num,
          name: ingredientName,
          measure: amount,
        }
        this.ingredients.push(item)
        console.log(this.ingredients)
      }

      // console.log(results.meals[0].strIngredient1)
      // console.log(meal.idMeal)
    },

    toggleModal() {
      this.showModal = !this.showModal
    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Sacramento&display=swap');
@import url('https://fonts.googleapis.com/css2?family=ABeeZee:ital@0;1&display=swap');

h1 {
  font-family: 'Sacramento', cursive;
  font-size: 70px;
  color: #ff4c00;
  margin-bottom: 0;
  margin-top: 250px;
}

h3 {
  margin: 40px 0 0;
}

.container {

}

.messagecontainer {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}

ul {
  margin-top: 50px;
  list-style-type: none;
  padding: 0;
}

li {
  margin: 0 10px;
}

a {
  color: #42b983;
}

img {
  width: 100px;
}

.results {
  margin: auto;
  max-width: 1335px;
}

.search {
  margin-top: 20px;
}

.error {
  font-size: 20px;
  color: dimgray;
  margin-top: 30px
}

.foodthumb {
  width: 100%;
  border-radius: 0px 0px 4px 4px;
  display: block;
}

.list-container {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
}

.card {
  background-color: white;
  flex-basis: 21%;
  overflow: hidden;
  box-shadow: 0px 2px 6px 1px rgba(0, 0, 0, 0.13), 0px 10px 15px 5px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
  border: white 2px solid;
  margin-top: 40px;
}

input {
  width: 250px;
  height: 40px;
  border-radius: 50px 0px 0px 50px;
  text-align: center;
  border: #ff4c00 1px solid;
  box-sizing: border-box;
  font-size: 16px;
}

button {
  width: 150px;
  height: 40px;
  border-radius: 0px 50px 50px 0px;
  background-color: #ff4c00;
  color: white;
  border: #ff4c00 1px solid;
  box-sizing: border-box;
}

@media (max-width: 1073px) {
  .card {
    flex-basis: 22%;
  }
}

@media (max-width: 815px) {
  .card {
    flex-basis: 30%;
  }
}

@media (max-width: 555px) {
  .card {
    flex-basis: 40%;
  }
}

</style>
