<template>
  <div>
    <div class="container-cards">
      <post-card v-for="post in paginatedItems" :key="post.id" :post="post" />
    </div>
    <div class="container-pagination">
      <v-pagination
        class="pagination"
        color="#38B6FF"
        v-model="pagination.page"
        :length="pagination.total"
        :total-visible="pagination.visible"
      ></v-pagination>
    </div>
  </div>
</template>

<script>
import PostCard from "../components/Post/PostCard.vue";

export default {
  name: "IndexPage",
  data() {
    return {
      cards: [],
      pagination: {
        page: 1,
        total: 0,
        perPage: 12,
        visible: 6,
      },
    };
  },
  components: {
    PostCard,
  },
  async mounted() {
    await this.getAll();
  },
  methods: {
    async getAll() {
      try {
        const response = await this.$axios.$get("/posts");

        this.cards = response;
        this.pagination.total = Math.ceil(
          this.cards.length / this.pagination.perPage
        );
      } catch (error) {
        throw new Error(error);
      }
    },
  },
  computed: {
    paginatedItems() {
      let page = this.pagination.page - 1;
      const perPage = this.pagination.perPage;
      let start = page * perPage;
      let end = start + perPage;

      const paginatedItems = this.cards;

      return paginatedItems.slice(start, end);
    },
  },
};
</script>

<style scoped>
.container-cards {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  max-width: 100%;
  margin-top: 20px;
}

.container-pagination {
  min-width: 100%;
  display: flex;
  justify-content: center;
}

.pagination {
  position: fixed;
  bottom: 0;
  margin-bottom: 20px;
}
</style>
