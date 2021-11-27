<template>
  <div>
    <h2 class="my-4">所有評論：</h2>

    <div v-for="comment in restaurantComments" :key="comment.id">
      <blockquote class="blockquote mb-0">
        <button
          v-if="currentUser.isAdmin"
          type="button"
          class="btn btn-danger float-right"
          @click.stop.prevent="handleDeleteButtonClick(comment.id)"
        >
          Delete
        </button>
        <h3>
          <a href="#">
            {{ comment.User.name }}
          </a>
        </h3>
        <p>{{ comment.text }}</p>
        <footer class="blockquote-footer">
          {{ comment.createdAt | fromNow }}
        </footer>
      </blockquote>
      <hr />
    </div>
  </div>
</template>

<script>
import { fromNowFilter } from "./../utils/mixins";
import { mapState } from "vuex";
import commentsAPI from "./../apis/comments";
import { Toast } from "./../utils/helper";

export default {
  name: "RestaurantComments",
  mixins: [fromNowFilter],
  props: {
    restaurantComments: {
      type: Array,
      required: true,
    },
  },
  computed: {
    ...mapState(["currentUser", "isAuthenticated"]),
  },
  methods: {
    async handleDeleteButtonClick(commentId) {
      try {
        const { data } = await commentsAPI.deleteComment({
          commentId,
        });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.$emit("after-delete-comment", commentId);
      } catch (error) {
        this.isProcessing = false;
        console.log("error", error);
        Toast.fire({
          icon: "error",
          title: "unable to delete comment atm",
        });
      }
    },
  },
};
</script>