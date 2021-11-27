<template>
  <div class="card mb-3">
    <div class="row no-gutters">
      <div class="col-md-4">
        <img :src="profile.image" width="300px" height="300px" />
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{ profile.name }}</h5>
          <p class="card-text">
            {{ profile.email }}
          </p>
          <ul class="list-unstyled list-inline">
            <li>
              <strong>{{ profile.commentsLength }}</strong> 已評論餐廳
            </li>
            <li>
              <strong>{{ profile.favoritedRestaurantsLength }}</strong>
              收藏的餐廳
            </li>
            <li>
              <strong>{{ profile.followingsLength }}</strong> followings
              (追蹤者)
            </li>
            <li>
              <strong>{{ profile.followersLength }}</strong> followers (追隨者)
            </li>
          </ul>
          <template v-if="isCurrentUser">
            <router-link
              :to="{ name: 'user-edit', params: { id: profile.id } }"
              class="btn btn-primary"
            >
              Edit
            </router-link>
          </template>
          <template v-else>
            <button
              v-if="isFollowed"
              @click.stop.prevent="unfollow(profile.id)"
              type="button"
              class="btn btn-danger btn-border favorite mr-2"
            >
              Unfollow
            </button>
            <button
              v-else
              @click.stop.prevent="follow(profile.id)"
              type="button"
              class="btn btn-primary btn-border favorite mr-2"
            >
              Follow
            </button>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import usersAPI from "./../apis/users";
import { Toast } from "./../utils/helper";

export default {
  props: {
    profile: {
      type: Object,
      required: true,
    },
    isCurrentUser: {
      type: Boolean,
      required: true,
    },
    initialIsFollowed: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      isFollowed: this.initialIsFollowed,
    };
  },
  watch: {
    initialIsFollowed(isFollowed) {
      this.isFollowed = isFollowed;
    },
  },
  methods: {
    async follow(userId) {
      try {
        const { data } = await usersAPI.addFollowing({ userId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.isFollowed = true;
        this.$router.go();
      } catch (error) {
        console.log("error", error);
        Toast.fire({
          icon: "error",
          title: "can't follow",
        });
      }
    },
    async unfollow(userId) {
      try {
        const { data } = await usersAPI.deleteFollowing({ userId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.isFollowed = false;
        this.$router.go();
      } catch (error) {
        console.log("error", error);
        Toast.fire({
          icon: "error",
          title: "can't unfollow",
        });
      }
    },
  },
};
</script>

