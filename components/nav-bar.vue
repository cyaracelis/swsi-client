<template>
  <v-toolbar elevation="4" color="#000080">
    <v-toolbar-title>
      <v-btn icon color="#FFFFFF" @click="home">
        <img src="~/assets/img/swsi_logo.png" class="logo" />
      </v-btn>
      Sinukuan Water System Inc.
    </v-toolbar-title>
    <v-spacer></v-spacer>
    <v-menu left bottom>
      <template #activator="{ on, attrs }">
        <v-btn icon v-bind="attrs" v-on="on" @click="about">
          <v-icon color="#FFFFFF"> mdi-menu </v-icon>
        </v-btn>
      </template>

      <v-list>
        <v-list-item v-for="n in 5" :key="n" @click="() => {}">
          <v-list-item-title>Option {{ n }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
  </v-toolbar>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  methods: {
    home() {
      this.$router.push('/')
    },
    about() {
      this.$router.push('/about')
    },
  },
})
</script>

<style lang="postcss" scoped>
.v-toolbar {
  background-color: #000080;
  z-index: 10;
}

.v-toolbar__title {
  font-family: 'Imprima', 'sans-serif';
  font-weight: 400;
  color: white;
}

.logo {
  width: 65px;
  height: 50px;
}
</style>