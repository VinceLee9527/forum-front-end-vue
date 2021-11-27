<template>
  <form @submit.stop.prevent="handleSubmit">
    <div class="form-group mb-4">
      <label for="text">留下評論：</label>
      <textarea class="form-control" rows="3" name="text" v-model="text" />
    </div>
    <div class="d-flex align-items-center justify-content-between">
      <button type="button" class="btn btn-link" @click="$router.back()">
        回上一頁
      </button>
      <button
        type="submit"
        class="btn btn-primary mr-0"
        :disabled="isProcessing"
      >
        Submit
      </button>
    </div>
  </form>
</template>

<script>
import commentsAPI from "./../apis/comments";
import { Toast } from "./../utils/helper";

export default {
  props: {
    restaurantId: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      text: "",
      isProcessing: false,
    };
  },
  methods: {
    async handleSubmit() {
      try {
        this.isProcessing = true;
        const { data } = await commentsAPI.postComment({
          restaurantId: this.restaurantId,
          text: this.text,
        });
        this.$emit("after-create-comment", {
          restaurantId: this.restaurantId,
          text: this.text,
        });
        this.isProcessing = false;
        this.text = "";
      } catch (error) {
        this.isProcessing = false;
        console.log("error", error);
        Toast.fire({
          icon: "error",
          title: "unable to leave comment atm",
        });
      }
    },
  },
};
</script>