<template>
  <div class="backdrop" @click="closeModal">
    <button @click="increment">test</button>

    <div class="modal">
      <div v-for="recipe in recipeResultsProp" :key="recipe">
        <h1>{{ recipe[0].strMeal }}</h1>
        <hr>
        <h4>Preparation</h4>
        <p> {{ recipe[0].strInstructions }}</p>
        <h4>Ingredients</h4>
        <table style="width:100%">
          <tr>
            <th>Ingredient</th>
            <th>Measure</th>
          </tr>
          <tr>
            <td>{{ recipe[0].strIngredient1 }}</td>
            <td>{{ recipe[0].strMeasure1 }}</td>
          </tr>
          <tr>
            <td>{{ recipe[0].strIngredient2 }}</td>
            <td>{{ recipe[0].strMeasure2 }}</td>
          </tr>
        </table>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: "RecipeModal",
  props: ["recipeResultsProp"],

  methods: {
    closeModal() {
      this.$emit("close")
    }
  }
}
</script>

<style scoped>

h1 {
}

hr {
  border: 1px solid #fdded1;
}

h4 {
  color: #ff4c00;
}

.modal {
  width: 800px;
  padding: 20px;
  margin: 100px auto;
  background: white;
  border-radius: 10px;
  white-space: break-spaces;
}

.backdrop {
  top: 0;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}

@media (max-width: 1073px) {
  .modal {
    width: 80%;
  }
}

@media (max-width: 815px) {
  .modal {
    width: 80%;
  }
}

@media (max-width: 555px) {
  .modal {
    width: 80%;
  }
}
</style>