<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">人氣餐廳</h1>

    <hr />
    <div
      class="card mb-3"
      style="max-width: 540px; margin: auto"
      v-for="restaurant in restaurants"
      :key="restaurant.id"
    >
      <div class="row no-gutters">
        <div class="col-md-4">
          <a href="#">
            <img class="card-img" :src="restaurant.image" />
          </a>
        </div>
        <div class="col-md-8">
          <div class="card-body">
            <h5 class="card-title">
              {{ restaurant.name }}
            </h5>
            <span class="badge badge-secondary"
              >收藏數：{{ restaurant.FavoriteCount }}</span
            >
            <p class="card-text">
              {{ restaurant.description }}
            </p>
            <router-link
              :to="{
                name: 'restaurantDashboard',
                params: { id: restaurant.id },
              }"
            >
              Show
            </router-link>

            <button
              v-if="restaurant.isFavorited"
              @click.prevent.stop="deleteFavorite(restaurant.id)"
              type="button"
              class="btn btn-danger mr-2"
            >
              移除最愛
            </button>
            <button
              v-else
              @click.prevent.stop="addFavorite(restaurant.id)"
              type="button"
              class="btn btn-primary"
            >
              加到最愛
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";
import restaurantsAPI from "./../apis/restaurants";
import usersAPI from "./../apis/users";
import { Toast } from "./../utils/helper";

export default {
  components: {
    NavTabs,
  },
  data() {
    return {
      restaurants: [],
    };
  },
  methods: {
    async fetchRes() {
      try {
        const { data } = await restaurantsAPI.getTopRestaurants();
        if (data.status === "error") {
          throw new Error(data.message);
        }
        this.restaurants = data.restaurants;
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法取得，請稍後再試",
        });
      }
    },
    async addFavorite(restaurantId) {
      try {
        const { data } = await usersAPI.addFavorite({ restaurantId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.restaurants = this.restaurants.map((restaurant) => {
          if (restaurant.id !== restaurantId) {
            return restaurant;
          } else {
            return {
              ...restaurant,
              FavoriteCount: restaurant.FavoriteCount + 1,
              isFavorited: true,
            };
          }
        });
      } catch (error) {
        console.log("error", error);
        Toast.fire({
          icon: "error",
          title: "can't add to favorite",
        });
      }
    },
    async deleteFavorite(restaurantId) {
      try {
        const { data } = await usersAPI.deleteFavorite({ restaurantId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.restaurants = this.restaurants.map((restaurant) => {
          if (restaurant.id !== restaurantId) {
            return restaurant;
          } else {
            return {
              ...restaurant,
              FavoriteCount: restaurant.FavoriteCount - 1,
              isFavorited: false,
            };
          }
        });
      } catch (error) {
        console.log("error", error);
        Toast.fire({
          icon: "error",
          title: "can't add to favorite",
        });
      }
    },
  },
  created() {
    this.fetchRes();
  },
};
</script>