<template>
  <RecipeModal recipe="test"/>
  <div class="hello">
    <img alt="food logo" src="@/assets/food-serving.png">
    <h1>{{ msg }}</h1>
  </div>

  <div class="search">
    <h2>{{ mealQuery }}</h2>
    <input v-model="mealQuery" placeholder="search by ingredient">
    <button @click="fetchFood">Search Food!</button>
  </div>

  <div v-if="errorMsg">
    {{ errorMsg }}
  </div>

  <div class="results">
    <div v-for="recipe in recipeResults" :key="recipe">
      <p> {{ recipe[0].strInstructions }}</p>
    </div>

    <ul class="list-container">
      <li class="card" @click="getRecipe(meal)" v-for="meal in mealResults.meals" :key="meal.idMeal">
        <h4>{{ meal.strMeal }}</h4>
        <img class="foodthumb" :src="meal.strMealThumb">
      </li>
    </ul>
  </div>

</template>

<script>
import RecipeModal from "./RecipeModal";

export default {
  name: 'HelloWorld',
  components: { RecipeModal },

  data() {
    return {
      mealQuery: "",
      msg: "Search for a recipe",
      mealResults: [],
      errorMsg: "",
      recipeResults: ""
    }
  },
  methods: {

    async fetchFood() {

      try {
        const response = await fetch(`https://www.themealdb.com/api/json/v1/1/filter.php?i=${this.mealQuery}`)

        const results = await response.json();
        this.mealResults = results

        // console.log(results)

      } catch (e) {
        this.errorMsg = `no food with ${this.mealQuery}`
        console.log('error')
      }
    },

    async getRecipe(meal) {
      console.log("it works")
      const response = await fetch(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${meal.idMeal}`)

      const results = await response.json();
      this.recipeResults = results

      console.log(results)
      console.log(meal.idMeal)

    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
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

.foodthumb {
  width: 100%;
  border-radius: 0px 0px 10px 10px;
  display: block;
}

.list-container {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
}

.card {
  flex-basis: 23%;
  overflow: hidden;
  box-shadow: 0 4px 21px -15px rgba(0, 0, 0, 0.75);
  border-radius: 10px;
  margin-top: 40px;
}

@media(max-width: 1073px) {
  .card {
    flex-basis: 30%;
  }
}@media(max-width: 815px) {
  .card {
    flex-basis: 45%;
  }
}@media(max-width: 555px) {
  .card {
    flex-basis: 100%;
  }
}

</style>
