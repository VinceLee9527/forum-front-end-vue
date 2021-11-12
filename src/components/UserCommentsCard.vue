<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ userComments.length }}</strong> 已評論餐廳
    </div>
    <div class="card-body">
      <router-link
        v-for="userComment in userComments"
        :key="userComment.id"
        :to="{ name: 'restaurant', params: { id: userComment.profile.id } }"
      >
        <img :src="userComment.profile.image" width="60" height="60" />
      </router-link>
    </div>
  </div>
</template>


<script>
export default {
  props: {
    userComments: {
      type: Array,
      required: true,
    },
  },
};
</script>