<template>
  <div class="container py-5">
    <!-- 餐廳資訊頁 RestaurantDetail -->
    <RestaurantsDetail :initialRestaurant="restaurant"/>
    <hr>
    <!-- 餐廳評論 RestaurantComments -->
    <RestaurantComments :restaurantComments="restaurantComments" @after-delete-comment="afterDeleteComment"/>
    <!-- 新增評論 CreateComment -->
    <CreateComment :restaurantId="restaurant.id" @after-create-comment="afterCreateComment"/>
  </div>
</template>

<script>
import RestaurantsDetail from './../components/RestaurantsDetail'
import RestaurantComments from './../components/RestaurantComments'
import CreateComment from './../components/CreateComment'


const dummyData = {
    "restaurant": {
        "id": 1,
        "name": "Dr. Ignacio Schaden",
        "tel": "1-117-260-8931",
        "address": "4699 Sanford Parkway",
        "opening_hours": "08:00",
        "description": "Odio dolores id tempore.\nIncidunt aut saepe voluptates in voluptatem non labore saepe.",
        "image": "https://loremflickr.com/320/240/restaurant,food/?random=64.80864812274613",
        "viewCounts": 1,
        "createdAt": "2021-11-07T16:49:43.000Z",
        "updatedAt": "2021-11-11T13:03:33.862Z",
        "CategoryId": 4,
        "Category": {
            "id": 4,
            "name": "墨西哥料理",
            "createdAt": "2021-11-07T16:49:43.000Z",
            "updatedAt": "2021-11-07T16:49:43.000Z"
        },
        "FavoritedUsers": [],
        "LikedUsers": [],
        "Comments": [
            {
                "id": 1,
                "text": "Quaerat praesentium occaecati et in harum sint ut rerum aspernatur.",
                "UserId": 1,
                "RestaurantId": 1,
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z",
                "User": {
                    "id": 1,
                    "name": "root",
                    "email": "root@example.com",
                    "password": "$2a$10$Otikzsjh3dtAowuHwk6apeTYu90k8KCo3KKkwdZ2MOpyLuRrn.Uea",
                    "isAdmin": true,
                    "image": null,
                    "createdAt": "2021-11-07T16:49:43.000Z",
                    "updatedAt": "2021-11-07T16:49:43.000Z"
                }
            },
            {
                "id": 101,
                "text": "Quaerat est nam cupiditate.",
                "UserId": 2,
                "RestaurantId": 1,
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z",
                "User": {
                    "id": 2,
                    "name": "user1",
                    "email": "user1@example.com",
                    "password": "$2a$10$RVKykLpJtzeBLDD7SDItuu4VAlzFaHZgYGQYFzB5AO3WyPX8Y6Cgq",
                    "isAdmin": false,
                    "image": null,
                    "createdAt": "2021-11-07T16:49:43.000Z",
                    "updatedAt": "2021-11-07T16:49:43.000Z"
                }
            },
            {
                "id": 51,
                "text": "Expedita porro dolores sit ab et voluptas molestiae sit quasi.",
                "UserId": 3,
                "RestaurantId": 1,
                "createdAt": "2021-11-07T16:49:43.000Z",
                "updatedAt": "2021-11-07T16:49:43.000Z",
                "User": {
                    "id": 3,
                    "name": "user2",
                    "email": "user2@example.com",
                    "password": "$2a$10$Q/sPM3ZZX0Y2aenhJxTTcuY58QBaelDePP5uaUbYq.vmJI7Iw2qxK",
                    "isAdmin": false,
                    "image": null,
                    "createdAt": "2021-11-07T16:49:43.000Z",
                    "updatedAt": "2021-11-07T16:49:43.000Z"
                }
            }
        ]
    },
    "isFavorited": false,
    "isLiked": false
}

const dummyUser = {
  currentUser: {
    id: 1,
    name: '管理者',
    email: 'root@example.com',
    image: 'https://i.pravatar.cc/300',
    isAdmin: true
  },
  isAuthenticated: true
}

export default {
  components: {
    RestaurantsDetail,
    RestaurantComments,
    CreateComment
  },
  data () {
    return {
      restaurant: {
        id: -1,
        name: '',
        categoryName: '',
        image: '',
        openingHours: '',
        tel: '',
        address: '',
        description: '',
        isFavorited: false,
        isLiked: false
      },
      restaurantComments: [],
      currentUser: dummyUser.currentUser
    }
  },
  created() {
    const { id } = this.$route.params
    this.fetchRestaurant(id)
  },
  methods: {
    fetchRestaurant (restaurantId) {
      console.log('fetchRestaurant id: ', restaurantId)

      this.restaurant = {
        id: dummyData.restaurant.id,
        name: dummyData.restaurant.name,
        categoryName: dummyData.restaurant.Category.name,
        image: dummyData.restaurant.image,
        openingHours: dummyData.restaurant.opening_hours,
        tel: dummyData.restaurant.tel,
        address: dummyData.restaurant.address,
        description: dummyData.restaurant.description,
        isFavorited: dummyData.isFavorited,
        isLiked: dummyData.isLiked,
      }

      this.restaurantComments = dummyData.restaurant.Comments
    },
    afterDeleteComment (commentId) {
      // 以 filter 保留未被選擇的 comment.id
      this.restaurantComments = this.restaurantComments.filter(
        comment => comment.id !== commentId
      )
    },
    afterCreateComment (payload) {
      const { commentId, restaurantId, text } = payload
      this.restaurantComments.push({
        id: commentId,
        RestaurantId: restaurantId,
        User: {
          id: this.currentUser.id,
          name: this.currentUser.name
        },
        text,
        createdAt: new Date()
      })
    }
  }
  
}
</script>