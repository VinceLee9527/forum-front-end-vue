<template>
  <div class="container py-5">
    <!-- AdminNav Component -->
    <AdminNav />

    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Email</th>
          <th scope="col">Role</th>
          <th scope="col" width="140">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <th scope="row">{{ user.id }}</th>
          <td>{{ user.email }}</td>
          <td v-show="user.isAdmin">admin</td>
          <td v-show="!user.isAdmin">user</td>
          <td>
            <button
              type="button"
              v-show="user.isAdmin"
              @click.stop.prevent="adminUserToggle(user.id)"
              class="btn btn-link"
            >
              set as user
            </button>
            <button
              type="button"
              v-show="!user.isAdmin"
              @click.stop.prevent="adminUserToggle(user.id)"
              class="btn btn-link"
            >
              set as admin
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import AdminNav from "./../components/AdminNav";

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
    },
  ],
};
export default {
  name: "adminUser",
  components: {
    AdminNav,
  },
  data() {
    return {
      users: [],
    };
  },
  created() {
    this.fetchAdminUsers();
  },
  methods: {
    fetchAdminUsers() {
      this.users = dummyData.users;
    },
    adminUserToggle(userId) {
      this.users = this.users.map((user) => {
        if (user.id === userId) {
          return {
            ...user,
            isAdmin: !user.isAdmin,
          };
        }
        return user;
      });
    },
  },
};
</script>
