<template>
  <div class="backdrop" @click="closeModal">

    <div class="modal">
      <div v-for="recipe in recipeResultsProp" :key="recipe">
        <h1>{{ recipe[0].strMeal }}</h1>
        <hr>
        <h4>Preparation</h4>
        <p> {{ recipe[0].strInstructions }}</p>
      </div>

      <h4>Ingredients</h4>
      <table style="width:100%">
        <tr>
          <th>Ingredient</th>
          <th>Measure</th>
        </tr>
        <tr v-for="it in ingredientsProp" :key="it.id">
          <td>{{ it.name }}</td>
          <td>{{ it.measure }}</td>
        </tr>
      </table>
    </div>
  </div>

</template>

<script>
export default {
  name: "RecipeModal",
  props: ["recipeResultsProp", "ingredientsProp", "ingredientProp"],

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
  padding: 20px;
  margin: 100px 40px;
  background: white;
  border-radius: 10px;
  white-space: break-spaces;
  max-height: 100%;
  overflow-y: auto;
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