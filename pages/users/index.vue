<template>
  <v-container style="max-width: max-content;">
    <v-list>
      <h1>Usuários</h1>

      <v-list-item v-for="user in users" :key="user.id">
        <v-avatar class="mr-3" color="#cecece" size="40">
          <v-icon x-large> mdi-account-circle </v-icon>
        </v-avatar>

        <v-list-item-content>
          <v-list-item-title>{{ user.name }}</v-list-item-title>
        </v-list-item-content>

        <v-list-item-action>
          <v-btn
            elevation="2"
            width="136"
            class="font-weight-regular text-capitalize hidden-sm-and-down"
            outlined
            tile
            color="#38B6FF"
            @click="openDetails(user)"
          >
            <v-icon color="#38B6FF" class="mr-3"> mdi-card-account-details </v-icon>
            Detalhes
          </v-btn>
        </v-list-item-action>
      </v-list-item>
    </v-list>
    <user-details :user="user" :dialog="dialog" @close-dialog="dialog = false"></user-details>
  </v-container>
</template>
<script>
import UserDetails from '../../components/User/UserDetails.vue';

export default {
  name: "IndexPage",
  data() {
    return {
      users: [],
      dialog: false,
      user: {}
    };
  },
  components: {
    UserDetails
  },
  async mounted() {
    await this.getAll();
  },
  methods: {
    async getAll() {
      try {
        const response = await this.$axios.$get("/users");

        this.users = response;
      } catch (error) {
        throw new Error(error);
      }
    },
    openDetails(user) {
      this.dialog = true;
      this.user = user;
    }
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
