<template>
  <v-container class="mt-2">
    <v-img
      lazy-src="https://picsum.photos/id/11/10/6"
      max-width="100%"
      max-height="420"
      src="https://picsum.photos/id/11/1080/920"
    ></v-img>
    <h1 class="mb-3">{{ post.title }}</h1>
    <span>{{ post.body }}</span>

    <v-divider />

    <h3 class="my-6">{{ comments.length }} Comentários</h3>
    <v-row v-for="comment in comments" :key="comment.id">
      <v-list>
        <v-list-item class="d-flex">
          <v-avatar  class="mt-3 mr-3 align-self-start" color="#cecece" size="40">
            <v-icon x-large> mdi-account-circle </v-icon>
          </v-avatar>

          <v-list-item-content>
              <div>
                <span class="ml-2 font-weight-medium font-italic">{{ comment.name }} -</span>
                <a class="font-italic" href="mailto:">{{ comment.email }}</a>
              </div>
              <div>
                {{ comment.body }}
              </div>
          </v-list-item-content>

        </v-list-item>
      </v-list>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      id: this.$route.params.id,
      post: {},
      comments: [],
    };
  },

  async created() {
    await this.getPost();
  },
  methods: {
    async getPost() {
      try {
        const response = await this.$axios.$get(`/posts/${this.id}`);
        const responseComments = await this.$axios.$get(
          `/posts/${this.id}/comments`
        );

        this.post = response;
        this.comments = responseComments;
      } catch (error) {
        throw new Error(error);
      }
    },
  },
};
</script>

<style scoped>
.container-cards {
  max-width: 100%;
  margin-top: 20px;
}
</style>
