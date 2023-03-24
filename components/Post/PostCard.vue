<template>
  <v-col cols="12" sm="12" md="4">
  <v-card
    class="mx-auto mb-2"
    style="cursor: pointer"
    width="320"
    height="200"
    tile
    @click="toPost()"
  >
    <v-img
      lazy-src="https://picsum.photos/id/11/10/6"
      max-width="320"
      max-height="120"
      src="https://picsum.photos/id/11/500/300"
    ></v-img>
    <v-card-title class="font-weight-medium" style="font-size: 12px">{{
      post.title
    }}</v-card-title>
  </v-card>
</v-col>
</template>

<script>
export default {
  name: "PostCard",
  props: {
    post: Object,
  },
  methods: {
    toPost() {
      this.$router.push({ path: `/post/${this.post.id}` });
    },
  },
};
</script>
