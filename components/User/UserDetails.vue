<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="600px">
      <v-card>
        <v-card-title>
          <span class="text-h5">Detalhes do usuário</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12" sm="6" md="6">
                <h3>Nome:</h3>
                <span> {{ user.name }} </span>
              </v-col>
              <v-col cols="12" sm="6" md="6">
                <h3>Username:</h3>
                <span> {{ user.username }} </span>
              </v-col>
              <v-col cols="12">
                <h3>Email:</h3>
                <a :href="`mailto:${user.email}`"> {{ user.email }} </a>
              </v-col>
              <v-col cols="12" sm="6" md="6">
                <h3>Telefone:</h3>
                <span> {{ user.phone }} </span>
              </v-col>
              <v-col cols="12" sm="6" md="6">
                <h3>Site:</h3>
                <a
                  :href='`http://${user.website}`'
                  target="_blank"
                  rel="noopener noreferrer"
                  >{{ user.website }}</a
                >
              </v-col>

              <v-col cols="12"
                v-if="user.address"
              >
                <v-expansion-panels>
                  <v-expansion-panel
                  >
                    <v-expansion-panel-header style="color: rgba(0, 0, 0, 0.6); font-size: 18px; font-weight: 700;">
                      Endereço
                    </v-expansion-panel-header>
                    <v-expansion-panel-content>
                      <v-row style="color: rgba(0, 0, 0, 0.6);">
                        <v-col cols="12" sm="6" md="6">
                          <h3>Rua:</h3>
                          <span> {{ user.address.street }} </span>
                        </v-col>
                        <v-col cols="12" sm="6" md="6">
                          <h3>Apartamento:</h3>
                          <span> {{ user.address.suite }} </span>
                        </v-col>
                        <v-col cols="12" sm="6" md="6">
                          <h3>Cidade:</h3>
                          <span> {{ user.address.city }} </span>
                        </v-col>
                        <v-col cols="12" sm="6" md="6">
                          <h3>CEP:</h3>
                          <span> {{ user.address.zipcode }} </span>
                        </v-col>
                      </v-row>
                    </v-expansion-panel-content>
                  </v-expansion-panel>
                </v-expansion-panels>
              </v-col>
              <v-col cols="12" v-if="user.company">
                <v-expansion-panels>
                  <v-expansion-panel
                  >
                    <v-expansion-panel-header style="color: rgba(0, 0, 0, 0.6); font-size: 18px; font-weight: 700;">
                      Empresa
                    </v-expansion-panel-header>
                    <v-expansion-panel-content>
                      <v-row style="color: rgba(0, 0, 0, 0.6);">
                        <v-col cols="12" sm="6" md="6">
                          <h3>Nome:</h3>
                          <span> {{ user.company.name }} </span>
                        </v-col>
                        <v-col cols="12" sm="6" md="6">
                          <h3>Slogan:</h3>
                          <span> {{ user.company.catchPhrase }} </span>
                        </v-col>
                        <v-col cols="12" sm="6" md="6">
                          <h3>Estratégia de negócio:</h3>
                          <span> {{ user.company.bs }} </span>
                        </v-col>
                      </v-row>
                    </v-expansion-panel-content>
                  </v-expansion-panel>
                </v-expansion-panels>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="closeDialog">
            <v-icon>mdi-close</v-icon>
            Fechar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>
<script>
export default {
  name: "UserDetails",
  props: {
    dialog: false,
    user: {
      type: Object,
      default: {},
    },
  },

  methods: {
    closeDialog() {
      this.dialog = false;
      this.$emit("close-dialog", false);
    },
  },
};
</script>
