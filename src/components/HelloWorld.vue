<template>

  <div class="container">
    <div v-if="showModal">
      <RecipeModal :recipe-results-prop="recipeResults" :ingredients-prop="ingredients" :mealTitle="mealTitle"
                   :preparation="preparation" :meal="meal" @close="toggleModal"/>
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
      <div class="error" v-if="errorMsg">
        {{ errorMsg }}
      </div>
    </div>




    <div v-if="show" class="results">
      <ul class="list-container">
        <li class="card" @click="getRecipe(meal); toggleModal()" v-for="meal in mealResults.meals" :key="meal.idMeal">
          <img class="foodthumb" :src="meal.strMealThumb">
          <h4>{{ meal.strMeal }}</h4>
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
      msg: "Search recipes",
      mealResults: [],
      errorMsg: "",
      recipeResults: [],
      showModal: false,
      meal: {},
      ingredients: [],
      show: false,
      mealTitle: "",
      preparation: "",
      mealThumb: ""
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
      // this.recipeResults = results;
      // console.log(results);

      this.meal = results.meals[0]
      console.log(results.meals[0])

      this.mealTitle = results.meals[0].strMeal
      this.preparation = results.meals[0].strInstructions
      // this.preparation = this.preparation.replace(/(\r\n|\n|\r)/gm,"");
      this.mealThumb = results.meals[0].strMealThumb

      this.ingredients.splice(0);
      let ingredientName = undefined
      let num = 1;

      while (ingredientName !== "") {

        ingredientName = this.meal[`strIngredient${num}`]
        let amount = this.meal[`strMeasure${num}`]

        const item = {id: num, name: ingredientName, measure: amount}
        this.ingredients.push(item)
        num++

      }
      console.log(this.ingredients)
      this.ingredients.pop()
      return this.ingredients

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
@import url('https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

h1 {
  font-family: 'Sacramento';
  font-size: 80px;
  color: #06c167;
  margin-bottom: 0;
  /*margin-top: 280px;*/
}

h2{
  font-weight: 600;
}

h3 {
  margin: 20px 0 0;
  font-weight: 400;
}

h4{
  font-weight: 600;
}

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  height: 75vh;
  /*margin-top: 70px;*/
}

.messagecontainer {
  display: flex;
  /*flex-wrap: wrap;*/
  flex-direction: column;
  width: 100%;
  margin-top: 68px;

}

ul {
  margin-top: 20px;
  list-style-type: none;
  padding: 0;
}

li {
  margin: 0 10px;
}

a {
  color: #06c167;
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
  padding: 0 10px;
}

.error {
  font-size: 20px;
  font-weight: 400;
  color: dimgray;
  /*margin-top: 20px*/
}

.foodthumb {
  width: 100%;
  border-radius: 4px 4px 0px 0px;
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
  cursor: pointer;
}

.card:hover{
  color: #06c167;
}

input {
  width: 250px;
  height: 40px;
  border-radius: 5px;
  text-align: center;
  border: #06c167 1px solid;
  box-sizing: border-box;
  font-size: 16px;
  margin-right: 5px;
  margin-bottom: 10px;
}

button {
  width: 150px;
  height: 40px;
  border-radius: 5px;
  background-color: #06c167;
  color: white;
  border: #06c167 1px solid;
  box-sizing: border-box;
  margin-left: 5px;
  cursor: pointer;
  margin-bottom: 10px;

}

button:hover{
  background-color: #05a257;
}

@media (max-width: 1280px) {
  .card {
    flex-basis: 22%;
  }

  /*h1 {*/
  /*  margin-top: 170px;*/
  /*}*/
}

@media (max-width: 1024px) {
  .card {
    flex-basis: 22%;
  }

  /*h1 {*/
  /*  margin-top: 200px;*/
  /*}*/
}

@media (max-width: 768px) {
  .card {
    flex-basis: 30%;
  }
  /*h1{*/
  /*  margin-top: 230px;*/
  /*}*/
}

@media (max-width: 576px) {
  h1 {
    /*margin-top: 120px;*/
    font-size: 55px;
  }

  .card {
    flex-basis: 40%;
  }
}


</style>
