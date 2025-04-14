
<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer">
      <v-list-item title="My Application" subtitle="Vuetify"></v-list-item>
      <v-divider></v-divider>
      <v-list>
        <v-list-item link title="List" to="/">
          <template v-slot:prepend>
            <v-icon>mdi-format-list-checks</v-icon>
          </template>
        </v-list-item>

        <v-list-item link title="About" to="/about">
          <template v-slot:prepend>
            <v-icon>mdi-information</v-icon>
          </template>
        </v-list-item>

        <v-list-item link title="My group" to="/my-group">
          <template v-slot:prepend>
            <v-icon>mdi-book-open-page-variant</v-icon>
          </template>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      color="teal-darken-4"
      image="https://picsum.photos/1920/1080?random" fixed>

      <template v-slot:image>
        <v-img
          gradient="to top right, rgba(19,84,122,.8), rgba(128,208,199,.8)"
        ></v-img>
      </template>

      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-app-bar-title>Application</v-app-bar-title>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>

    </v-app-bar>


    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from 'vue'

const drawer = ref(null)
</script>

