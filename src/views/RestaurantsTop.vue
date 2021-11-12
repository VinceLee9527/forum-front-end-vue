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
              >收藏數：{{ restaurant.viewCounts }}</span
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

const dummyData = {
  restaurants: [
    {
      id: 1,
      name: "Dr. Ignacio Schaden",
      tel: "1-117-260-8931",
      address: "4699 Sanford Parkway",
      opening_hours: "08:00",
      description: "Odio dolores id tempore.\nIncidunt aut saepe volupt",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=64.80864812274613",
      viewCounts: 1,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-11T13:03:33.000Z",
      CategoryId: 4,
      Favoritedrestaurants: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 22,
      name: "Gillian Dickens",
      tel: "(041) 106-5319",
      address: "2480 Beer Pines",
      opening_hours: "08:00",
      description: "Doloremque sunt illum quia.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=78.47472623752823",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Favoritedrestaurants: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 23,
      name: "Dianna Osinski V",
      tel: "730.701.3131 x85683",
      address: "54975 Bode Motorway",
      opening_hours: "08:00",
      description: "Aperiam aspernatur ut iusto placeat laborum et id ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=21.6994683198134",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 1,
      Favoritedrestaurants: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 24,
      name: "Jess Kautzer",
      tel: "827-836-2135",
      address: "8540 Huels Bridge",
      opening_hours: "08:00",
      description: "Et qui est officiis alias qui ut facere.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=16.16602312774782",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Favoritedrestaurants: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 25,
      name: "Eden Heller",
      tel: "(291) 972-5214 x06680",
      address: "32989 Hirthe Gateway",
      opening_hours: "08:00",
      description: "Est molestiae reprehenderit alias laudantium quia ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=19.618933650219226",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Favoritedrestaurants: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 21,
      name: "Ellen Mraz",
      tel: "146-872-4399 x8994",
      address: "759 Israel Bridge",
      opening_hours: "08:00",
      description: "maiores vero deserunt",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=28.283026883839966",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Favoritedrestaurants: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 27,
      name: "Neal Mills",
      tel: "1-378-412-1624 x93771",
      address: "0803 Cruickshank Point",
      opening_hours: "08:00",
      description: "dolores qui et",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=8.294942495766211",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 1,
      Favoritedrestaurants: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 28,
      name: "Euna Rowe",
      tel: "1-716-708-5642",
      address: "27069 Champlin Summit",
      opening_hours: "08:00",
      description: "harum",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=94.66661135472425",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Favoritedrestaurants: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 29,
      name: "Roma Romaguera",
      tel: "702.960.3496",
      address: "016 Fredrick Hill",
      opening_hours: "08:00",
      description: "voluptatem",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=31.569986212483904",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 2,
      Favoritedrestaurants: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 30,
      name: "Cyrus O'Keefe",
      tel: "852.790.3124 x9485",
      address: "820 Holden Heights",
      opening_hours: "08:00",
      description: "Consequuntur delectus dolor ex earum qui eius enim",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=26.964421319947384",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Favoritedrestaurants: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
  ],
};

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
    fetchRes() {
      this.restaurants = dummyData.restaurants;
    },
    addFavorite(id) {
      for (let i = 0; i < this.restaurants.length; i++) {
        if (this.restaurants[i].id === id) {
          this.restaurants[i].isFavorited = true;
          return;
        }
      }
    },
    deleteFavorite(id) {
      for (let i = 0; i < this.restaurants.length; i++) {
        if (this.restaurants[i].id === id) {
          this.restaurants[i].isFavorited = false;
          return;
        }
      }
    },
  },
  created() {
    this.fetchRes();
  },
};
</script>