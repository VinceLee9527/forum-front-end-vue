<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ favorited.length }}</strong> 收藏的餐廳
    </div>
    <div class="card-body">
      <router-link
        v-for="favorite in favorited"
        :key="favorite.id"
        :to="{ name: 'restaurant', params: { id: favorite.id } }"
      >
        <img :src="favorite.image" width="60" height="60" />
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    favorited: {
      type: Array,
      required: true,
    },
  },
};
</script>