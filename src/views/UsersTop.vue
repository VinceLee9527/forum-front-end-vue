<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">美食達人</h1>
    <hr />
    <div class="row text-center">
      <div class="col-3" v-for="user in users" :key="user.id">
        <router-link :to="{ name: 'user', params: { id: user.id } }">
          <img :src="user.image" width="140px" height="140px" />
        </router-link>
        <h2>{{ user.name }}</h2>
        <span class="badge badge-secondary bg-black"
          >追蹤人數：{{ user.FollowerCount }}</span
        >
        <p class="mt-3">
          <button
            type="button"
            class="btn btn-danger"
            @click.stop.prevent="deleteFollow(user.id)"
            v-if="user.isFollowed"
          >
            取消追蹤
          </button>
          <button
            type="button"
            class="btn btn-primary"
            @click.stop.prevent="addFollow(user.id)"
            v-else
          >
            追蹤
          </button>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";

const dummyData = {
  users: [
    {
      id: 1,
      name: "root",
      email: "root@example.com",
      password: "$2a$10$Otikzsjh3dtAowuHwk6apeTYu90k8KCo3KKkwdZ2MOpyLuRrn.Uea",
      isAdmin: true,
      image: null,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
    {
      id: 2,
      name: "user1",
      email: "user1@example.com",
      password: "$2a$10$RVKykLpJtzeBLDD7SDItuu4VAlzFaHZgYGQYFzB5AO3WyPX8Y6Cgq",
      isAdmin: false,
      image: null,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
    {
      id: 3,
      name: "user2",
      email: "user2@example.com",
      password: "$2a$10$Q/sPM3ZZX0Y2aenhJxTTcuY58QBaelDePP5uaUbYq.vmJI7Iw2qxK",
      isAdmin: false,
      image: null,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
  ],
};
export default {
  name: "users",
  components: {
    NavTabs,
  },
  data() {
    return {
      users: [],
    };
  },
  methods: {
    fetchUsers() {
      this.users = dummyData.users;
    },
    addFollow(id) {
      for (let i = 0; i < this.users.length; i++) {
        if (this.users[i].id === id) {
          this.users[i].isFollowed = true;
          return;
        }
      }
    },
    deleteFollow(id) {
      for (let i = 0; i < this.users.length; i++) {
        if (this.users[i].id === id) {
          this.users[i].isFollowed = false;
          return;
        }
      }
    },
  },
  created() {
    this.fetchUsers();
  },
};
</script>