<script setup lang="ts">
import { ref } from "vue";

interface Restaurant {
  name?: string;
  status?: RestaurantStatus;
  dishes?: Dish[];
}

type RestaurantStatus =
  | "Want to Try"
  | "Recommended"
  | "Do not Recommend"
  | "Must Try";

const restaurantList = ref<Restaurant[]>([]);
const newResaurant = ref<Restaurant>({});

const statusList = [
  "Want to Try",
  "Recommended",
  "Do Not Recommend",
  "Must Try",
];

const addRestaurant = () => {
  restaurantList.value.push({
    name: newResaurant.value.name,
    status: "Want to Try",
    dishes: [],
  });
};
</script>

<template>
  <main>
    <pre>
      {{ newResaurant }}
    </pre>
    <!-- Create a form that allows users to add a restaurant to a list -->
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input id="restaurant-name" v-model="newResaurant.name" type="text" />
      </div>
      <div>
        <label for="restaurant-status">Restaurant Status</label>
        <input
          id="restaurant-status"
          v-model="newResaurant.status"
          type="text"
        />
      </div>
      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">
        {{ restaurant.name }}
      </li>
    </ul>
  </main>
</template>
