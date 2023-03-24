<template>
  <div>
    <v-navigation-drawer
      v-model="drawer"
      temporary
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-subtitle
            style="font-weight: 500; font-size: 14px; letter-spacing: 1px;"
          >
            MENU
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>
      <v-list nav>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon color="#38B6FF">{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>{{item.title}}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar class="hidden-sm-and-down" fixed app height="80">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <div >
        <NuxtLink to="/"
          >Blog</NuxtLink>
      </div>
      <v-spacer />
      <home-button class="mr-6" />
    </v-app-bar>
    <v-app-bar class="hidden-xs-and-up" fixed app height="80">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <div ><img
          src="../assets/icons8-blog-64.png"
          alt="Logo Blog"
          width="140"
          class="mr-2 mt-4"
      />
      </div>
      <v-spacer />
      <home-button />
    </v-app-bar>
  </div>
</template>

<script>
import HomeButton from './Buttons/HomeButton.vue'

export default {
  name: 'Header',
  components: {
    HomeButton
  },
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-post',
          title: 'Postagens',
          to: '/'
        },
        {
          icon: 'mdi-account',
          title: 'Usuários',
          to: '/users'
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'SUTHUB'
    }
  }
}
</script>
