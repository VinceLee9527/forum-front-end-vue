<template>
  <div class="container py-5">
    <NavTabs />

    <!-- nav pills -->
    <RestaurantsNavPills :categories="categories"/>
    <div class="row">
      <RestaurantCard v-for="restaurant in restaurants" :key="restaurant.id" :initialRestaurant="restaurant"/>
    </div>

<!-- pagination -->
<RestaurantsPagination
      v-if="totalPage.length > 1"
      :current-page="currentPage"
      :total-page="totalPage"
      :category-id="categoryId"
      :previous-page="previousPage"
      :next-page="nextPage"
    />

  </div>
</template>

<script>
import NavTabs from './../components/NavTabs'
import RestaurantCard from './../components/RestaurantCard'
import RestaurantsNavPills from './../components/RestaurantsNavPills'
import RestaurantsPagination from './../components/RestaurantsPagination'

const dummyData= {
    "restaurants": [
        {
            "id": 1,
            "name": "Dr. Ignacio Schaden",
            "tel": "1-117-260-8931",
            "address": "4699 Sanford Parkway",
            "opening_hours": "08:00",
            "description": "Odio dolores id tempore.\nIncidunt aut saepe volupt",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=64.80864812274613",
            "viewCounts": 0,
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z",
            "CategoryId": 4,
            "Category": {
                "id": 4,
                "name": "墨西哥料理",
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 2,
            "name": "Shyanne Schamberger",
            "tel": "(415) 455-8000 x0053",
            "address": "45155 Leonie Forge",
            "opening_hours": "08:00",
            "description": "reiciendis est officia",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=26.95346949336752",
            "viewCounts": 0,
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z",
            "CategoryId": 3,
            "Category": {
                "id": 3,
                "name": "義大利料理",
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 3,
            "name": "Erika Kohler",
            "tel": "688.166.1376",
            "address": "6274 Leonora Glens",
            "opening_hours": "08:00",
            "description": "Nisi voluptatem odit quam atque esse qui. Et et qu",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=89.09004118949329",
            "viewCounts": 0,
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z",
            "CategoryId": 2,
            "Category": {
                "id": 2,
                "name": "日本料理",
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 4,
            "name": "Dr. Joanne Schiller",
            "tel": "139.032.1777",
            "address": "59479 Balistreri Drive",
            "opening_hours": "08:00",
            "description": "veritatis",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=25.116136783468445",
            "viewCounts": 0,
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z",
            "CategoryId": 2,
            "Category": {
                "id": 2,
                "name": "日本料理",
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 5,
            "name": "Icie Little",
            "tel": "1-008-084-8081 x679",
            "address": "889 Blanda Unions",
            "opening_hours": "08:00",
            "description": "At quia dicta vel magnam et ut perspiciatis offici",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=87.74422300180635",
            "viewCounts": 0,
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z",
            "CategoryId": 5,
            "Category": {
                "id": 5,
                "name": "素食料理",
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 6,
            "name": "Royce Cummerata",
            "tel": "113.997.3143",
            "address": "626 Timmothy Roads",
            "opening_hours": "08:00",
            "description": "voluptatem rerum sint",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=38.4752127607771",
            "viewCounts": 0,
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z",
            "CategoryId": 4,
            "Category": {
                "id": 4,
                "name": "墨西哥料理",
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 7,
            "name": "Priscilla Weimann",
            "tel": "413-275-8040 x8807",
            "address": "13397 Boyd Springs",
            "opening_hours": "08:00",
            "description": "Et adipisci culpa. Repellat et qui alias ut iste e",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=93.76182351773355",
            "viewCounts": 0,
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z",
            "CategoryId": 1,
            "Category": {
                "id": 1,
                "name": "中式料理",
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 8,
            "name": "Otilia Funk",
            "tel": "1-824-643-8935 x81767",
            "address": "294 Schiller Key",
            "opening_hours": "08:00",
            "description": "Laboriosam voluptatum rerum illo ut ullam ut repel",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=9.915371048241429",
            "viewCounts": 0,
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z",
            "CategoryId": 3,
            "Category": {
                "id": 3,
                "name": "義大利料理",
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 9,
            "name": "Dr. Marina Hilll",
            "tel": "(583) 898-7076",
            "address": "853 O'Keefe Course",
            "opening_hours": "08:00",
            "description": "Et rerum omnis animi velit enim.\nAt pariatur molli",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=14.825573329294905",
            "viewCounts": 0,
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z",
            "CategoryId": 4,
            "Category": {
                "id": 4,
                "name": "墨西哥料理",
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 10,
            "name": "Alisha Terry III",
            "tel": "(015) 052-0301",
            "address": "33064 Labadie Square",
            "opening_hours": "08:00",
            "description": "cum",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=75.86577157393457",
            "viewCounts": 0,
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z",
            "CategoryId": 1,
            "Category": {
                "id": 1,
                "name": "中式料理",
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        }
    ],
    "categories": [
        {
            "id": 1,
            "name": "中式料理",
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z"
        },
        {
            "id": 2,
            "name": "日本料理",
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z"
        },
        {
            "id": 3,
            "name": "義大利料理",
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z"
        },
        {
            "id": 4,
            "name": "墨西哥料理",
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z"
        },
        {
            "id": 5,
            "name": "素食料理",
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z"
        },
        {
            "id": 6,
            "name": "美式料理",
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z"
        },
        {
            "id": 7,
            "name": "複合式料理",
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z"
        }
    ],
    "categoryId": "",
    "page": 1,
    "totalPage": [
        1,
        2,
        3,
        4,
        5
    ],
    "prev": 1,
    "next": 2
}
export default {
  components: {
    NavTabs,
    RestaurantCard,
    RestaurantsNavPills,
    RestaurantsPagination
  },
  data () {
    return {
      restaurants: [],
      categories: [],
      categoryId: -1,
      currentPage: 1,
      totalPage: [],
      previousPage: -1,
      nextPage: -1

    }
  },
  created(){
    this.fetchRestaurants()
  },
  methods: {
    fetchRestaurants () {
      const {
        restaurants,
        categories,
        categoryId,
        page,
        totalPage,
        prev,
        next
      } = dummyData
      this.restaurants = restaurants
      this.categories = categories
      this.categoryId = categoryId
      this.currentPage = page
      this.totalPage = totalPage
      this.previousPage = prev
      this.nextPage = next
    }

  }
}
</script>