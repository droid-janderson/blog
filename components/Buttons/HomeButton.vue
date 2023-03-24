<template>
  <div>
    <v-btn
      elevation="2"
      width="136"
      class="font-weight-regular text-capitalize hidden-sm-and-down"
      outlined
      tile
      color="#38B6FF"
      @click="toHome()"
    >
      <v-icon color="#38B6FF" class="mr-3">
        mdi-home
      </v-icon>
      Início
    </v-btn>
    <v-btn
      elevation="0"
      width="40"
      class="font-weight-regular text-capitalize hidden-sm-and-up"
      @click="toHome()"
    >
      <v-icon color="#38B6FF">
        mdi-home
      </v-icon>
    </v-btn>
  </div>
</template>

<script>
export default {
  name: 'HomeButton',
  methods: {
    toHome () {
      this.$router.push({ path: '/' })
    }
  }
}
</script>
