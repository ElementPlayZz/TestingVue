<script setup lang="ts">
import {ref} from "vue";

interface Restaurant{
  name?: string
  status?: RestaurantStatus
  dishes?: Dish[]
}

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

type RestaurantStatus = keyof typeof RestaurantStatusEnum

enum RestaurantStatusEnum{
  'Do Not Recommend' = -1,
  'Want to Try' = 0,
  'Recommended' = 1,
  'Must Try' = 2
}

enum RecommendStatus{
  'Do Not Recommend' = -1,
  'Want to Try' = 0,
  'Recommended' = 1,
  'Must Try' = 2
}

const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})

function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    status: newRestaurant.value.status,
    dishes: [],
  })
}
</script>

<template>
  <main>
    <pre>
      {{ newRestaurant }}
    </pre>
    <form @submit.prevent="addRestaurant">
    <div>
          <label for="restaurant-name">Restaurant Name</label>
    <input id="restaurant-name" v-model="newRestaurant.name" type="text"/>
      </div>

      <div>
        <label for="restaurant-status">Restaurant Status</label>
        <select name ="restaurant-status" id="restaurant-status" v-model="newRestaurant.status">
          <option v-for="status in Object.keys(RestaurantStatusEnum).filter(t=>!isNaN(Number(RestaurantStatusEnum[t])))" :value="status" :key="status"> {{status}} </option>
        </select>
      </div>

      <div>
        <label for="restaurant-diet">Restaurant Diet</label>
        <select name ="restaurant-status" id="restaurant-status" v-model="newRestaurant.status">
          <option v-for="status in Object.keys(RestaurantStatusEnum).filter(t=>!isNaN(Number(RestaurantStatusEnum[t])))" :value="status" :key="status"> {{status}} </option>
        </select>
      </div>

    <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList"
      :key="restaurant.name">
        {{ restaurant.name   }} - {{ restaurant.status }}
      </li>
    </ul>
  </main>
</template>
