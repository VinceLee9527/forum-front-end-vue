<template>
  <div class="container py-5">
    <form @submit.prevent.stop="handleSubmit">
      <div class="form-group">
        <label for="name">Name</label>
        <input
          v-model="name"
          id="name"
          type="text"
          name="name"
          class="form-control"
          placeholder="Enter Name"
          required
        />
      </div>

      <div class="form-group">
        <label for="image">Image</label>
        <img
          v-if="image"
          :src="image"
          class="d-block img-thumbnail mb-3"
          width="200"
          height="200"
        />
        <input
          id="image"
          type="file"
          name="image"
          accept="image/*"
          class="form-control-file"
          @change="handleFileChange"
        />
      </div>

      <button type="submit" class="btn btn-primary" :disabled="isProcessing">
        Submit
      </button>
    </form>
  </div>
</template>

<script>
import usersAPI from "./../apis/users";
import { Toast } from "./../utils/helper";
import { mapState } from "vuex";

export default {
  data() {
    return {
      id: -1,
      name: "",
      image: "",
      isProcessing: false,
    };
  },
  watch: {
    currentUser(user) {
      if (user.id === -1) return;
      const { id } = this.$route.params;
      this.setUser(id);
    },
  },
  created() {
    if (this.currentUser.id === -1) return;
    const { id } = this.$route.params;
    this.setUser(id);
  },
  computed: {
    ...mapState(["currentUser"]),
  },
  methods: {
    async handleSubmit(e) {
      try {
        this.isProcessing = true;
        const form = e.target; // <form></form>
        const formData = new FormData(form);

        const { data } = await usersAPI.update({
          userId: this.id,
          formData,
        });
        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.$router.push({ name: "user", params: { id: this.id } });
      } catch (error) {
        this.isProcessing = false;
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法取得人，請稍後再試",
        });
      }
    },
    setUser(userId) {
      const { id, name, image } = this.currentUser;

      if (id.toString() !== userId.toString()) {
        this.$router.push({ name: "not-found" });
        return;
      }

      this.id = id;
      this.name = name;
      this.image = image;
    },
    handleFileChange(e) {
      const { files } = e.target;
      if (files.length === 0) {
        this.image = "";
      } else {
        const imgURL = window.URL.createObjectURL(files[0]);
        this.image = imgURL;
      }
    },
  },
};
</script>



