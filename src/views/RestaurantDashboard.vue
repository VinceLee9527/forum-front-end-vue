<template>
  <div class="container py-5">
    <NavTabs />
    <div>
      <h1>{{ restaurant.name }}</h1>
      <span class="badge badge-secondary mt-1 mb-3">
        {{ restaurant.Category.name }}
      </span>
    </div>

    <hr />

    <ul>
      <li>評論數： {{ restaurant.Comments.length }}</li>
      <li>瀏覽次數： {{ restaurant.viewCounts }}</li>
    </ul>

    <button type="button" class="btn btn-link" @click="$router.back()">
      回上一頁
    </button>
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";

const dummyData = {
  restaurant: {
    id: 1,
    name: "Dr. Ignacio Schaden",
    tel: "1-117-260-8931",
    address: "4699 Sanford Parkway",
    opening_hours: "08:00",
    description:
      "Odio dolores id tempore.\nIncidunt aut saepe voluptates in voluptatem non labore saepe.",
    image:
      "https://loremflickr.com/320/240/restaurant,food/?random=64.80864812274613",
    viewCounts: 1,
    createdAt: "2021-11-07T16:49:43.000Z",
    updatedAt: "2021-11-11T13:03:33.000Z",
    CategoryId: 4,
    Category: {
      id: 4,
      name: "墨西哥料理",
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
    },
    Comments: [
      {
        id: 1,
        text: "Quaerat praesentium occaecati et in harum sint ut rerum aspernatur.",
        UserId: 1,
        RestaurantId: 1,
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$Otikzsjh3dtAowuHwk6apeTYu90k8KCo3KKkwdZ2MOpyLuRrn.Uea",
          isAdmin: true,
          image: null,
          createdAt: "2021-11-07T16:49:43.000Z",
          updatedAt: "2021-11-07T16:49:43.000Z",
        },
      },
      {
        id: 101,
        text: "Quaerat est nam cupiditate.",
        UserId: 2,
        RestaurantId: 1,
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
        User: {
          id: 2,
          name: "user1",
          email: "user1@example.com",
          password:
            "$2a$10$RVKykLpJtzeBLDD7SDItuu4VAlzFaHZgYGQYFzB5AO3WyPX8Y6Cgq",
          isAdmin: false,
          image: null,
          createdAt: "2021-11-07T16:49:43.000Z",
          updatedAt: "2021-11-07T16:49:43.000Z",
        },
      },
      {
        id: 51,
        text: "Expedita porro dolores sit ab et voluptas molestiae sit quasi.",
        UserId: 3,
        RestaurantId: 1,
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
        User: {
          id: 3,
          name: "user2",
          email: "user2@example.com",
          password:
            "$2a$10$Q/sPM3ZZX0Y2aenhJxTTcuY58QBaelDePP5uaUbYq.vmJI7Iw2qxK",
          isAdmin: false,
          image: null,
          createdAt: "2021-11-07T16:49:43.000Z",
          updatedAt: "2021-11-07T16:49:43.000Z",
        },
      },
    ],
  },
};

export default {
  name: "RestaurantDashboard",
  components: {
    NavTabs,
  },
  data() {
    return {
      restaurant: {},
    };
  },
  methods: {
    fetchRes() {
      this.restaurant = dummyData.restaurant;
    },
  },
  created() {
    this.fetchRes();
  },
};
</script>