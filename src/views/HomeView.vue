<script setup lang="ts">
import { ref } from 'vue'

interface Dish {
  name: string
  price: number
}

interface Restaurant {
  name: string
  address: string
  status: RestaurantStatus
  dishes: Dish[]
}

type RestaurantStatus = 'want to try' | 'Recommended' | 'try next time' | 'never go back'

const restaurantStatus = ['want to try', 'Recommended', 'try next time', 'never go back'] as const

const restaurants = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({ name: '', address: '', status: 'Recommended', dishes: [] })
function addRestaurant() {
  restaurants.value.push(newRestaurant.value)
  newRestaurant.value.name = ''
}
</script>

<template>
  <main>
    <pre>
      {{ newRestaurant }}
    </pre>
    <!-- create a form that allows users to add a restaurant -->
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="name">Name: </label>
        <input type="text" id="name" name="name" v-model="newRestaurant.name" />
      </div>
      <div>
        <label for="address">Address: </label>
        <input type="text" id="address" name="address" v-model="newRestaurant.address" />
      </div>
      <div>
        <label for="status">Status: </label>
        <select id="status" name="status" v-model="newRestaurant.status">
          <option v-for="status in restaurantStatus" :key="status" :value="status">
            {{ status }}
          </option>
        </select>
      </div>
      <button type="submit">Add</button>
    </form>

    <ul>
      <li v-for="restaurant in restaurants" :key="restaurant.name">{{ restaurant.name }}</li>
    </ul>
  </main>
</template>
