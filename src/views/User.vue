<template>
  <div class="album py-5 bg-light">
    <div class="container">
      <!-- user card -->
      <UserProfileCard
        :profile="profile"
        :is-current-user="currentUser.id === profile.id"
        :initial-is-followed="isFollowed"
      />

      <div class="row">
        <div class="col-md-4">
          <!-- follower card -->
          <UserFollowingsCard :followings="followings" />

          <!-- following card -->
          <br />
          <UserFollowersCard :followers="followers" />
        </div>
        <div class="col-md-8">
          <!-- commented restaurant card -->
          <UserCommentsCard :userComments="userComments" />

          <br />
          <UserFavoritedRestaurantsCard :favorited="favoritedRestaurants" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UserProfileCard from "./../components/UserProfileCard";
import UserFollowingsCard from "./../components/UserFollowingsCard";
import UserFollowersCard from "./../components/UserFollowersCard";
import UserCommentsCard from "./../components/UserCommentsCard";
import UserFavoritedRestaurantsCard from "./../components/UserFavoritedRestaurantsCard";
import usersAPI from "./../apis/users";
import { Toast } from "./../utils/helper";
import { mapState } from "vuex";

export default {
  name: "user",
  components: {
    UserProfileCard,
    UserFollowingsCard,
    UserFollowersCard,
    UserCommentsCard,
    UserFavoritedRestaurantsCard,
  },
  data() {
    return {
      profile: {
        id: 0,
        name: "",
        email: "",
        image: "",
        followingsLength: 0,
        followersLength: 0,
        commentsLength: 0,
        favoritedRestaurantsLength: 0,
      },
      userComments: [],
      followers: [],
      followings: [],
      favoritedRestaurants: [],
      isFollowed: false,
    };
  },
  computed: {
    ...mapState(["currentUser"]),
  },
  methods: {
    async fetchUser(userId) {
      try {
        const { data } = await usersAPI.get({
          userId,
        });
        const { profile, isFollowed } = data;

        const {
          id,
          image,
          name,
          email,
          Followings,
          Followers,
          Comments,
          FavoritedRestaurants,
        } = profile;

        this.profile = {
          ...this.profile,
          id,
          image,
          name,
          email,
          followingsLength: Followings.length,
          followersLength: Followers.length,
          commentsLength: Comments ? Comments.length : 0,
          favoritedRestaurantsLength: FavoritedRestaurants.length,
        };
        this.isFollowed = isFollowed;
        this.followings = Followings;
        this.followers = Followers;
        this.favoritedRestaurants = FavoritedRestaurants;
        this.userComments = Comments;
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法取得人，請稍後再試",
        });
      }
    },
  },
  beforeRouteUpdate(to, from, next) {
    const { id } = to.params;
    this.fetchUser(id);
    next();
  },
  created() {
    const { id } = this.$route.params;
    this.fetchUser(id);
  },
};
</script>