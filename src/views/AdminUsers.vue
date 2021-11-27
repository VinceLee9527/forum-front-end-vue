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
              @click.stop.prevent="
                adminUserToggle({ userId: user.id, isAdmin: user.isAdmin })
              "
              class="btn btn-link"
            >
              set as user
            </button>
            <button
              type="button"
              v-show="!user.isAdmin"
              @click.stop.prevent="
                adminUserToggle({ userId: user.id, isAdmin: user.isAdmin })
              "
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
import adminAPI from "./../apis/admin";
import { Toast } from "./../utils/helper";
import { mapState } from "vuex";

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
  computed: {
    ...mapState(["currentUser"]),
  },
  methods: {
    async fetchAdminUsers() {
      try {
        const { data } = await adminAPI.users.get();
        this.users = data.users;
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法取得人，請稍後再試",
        });
      }
    },
    async adminUserToggle({ userId, isAdmin }) {
      try {
        const { data } = await adminAPI.users.update({
          userId,
          isAdmin: (!isAdmin).toString(),
        });
        console.log("gang");

        if (data.status === "error") {
          throw new Error(data.message);
        }
        this.users = this.users.map((user) => {
          if (user.id === userId) {
            return {
              ...user,
              isAdmin: !isAdmin,
            };
          }
          return user;
        });
      } catch (error) {
        console.error(error.message);
        Toast.fire({
          icon: "error",
          title: "無法更新會員角色，請稍後再試",
        });
      }
    },
  },
};
</script>
