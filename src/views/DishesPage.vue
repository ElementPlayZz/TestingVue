<script setup lang="ts">
import {ref} from "vue";

interface Dish{
  name: string,
  diet?: Diet
  status?: RecommendStatus

}

type RestaurantDietStatus = keyof typeof RestaurantDiet
enum RestaurantDiet{
  'vegetarian' = 1,
  'vegan' = 2,
  'gluten-free' = 3,
  'pescatarin' = 4,
  'lactose-free' = 5,
  'other' = -1
}

const dishList = ref<Dish[]>([])
const newDish = ref<Dish>({})

function addDish() {
  dishList.value.push({
    name: newDish.value.name,
    status: newDish.value.status
  })
}
</script>

<template>
  <main>
    <pre>
      {{ newDish }}
    </pre>
    <form @submit.prevent="addDish">
      <div>
        <label for="dish-name">Dish Name</label>
        <input id="dish-name" v-model="newDish.name" type="text"/>
      </div>

      <div>
        <label for="dish-name">Dish Status</label>
        <select name ="dish-status" id="dish-name" v-model="newDish.status">
          <option v-for="status in Object.keys(RestaurantDiet).filter(t=>!isNaN(Number(RestaurantDiet[t])))" :value="status" :key="status"> {{status}} </option>
        </select>
      </div>

      <button type="submit">Add Dish</button>
    </form>
    <ul>
      <li v-for="Dish in dishList"
          :key="Dish.name">
        {{ Dish.name   }} - {{ Dish.status }}
      </li>
    </ul>
  </main>
</template>
