<template>
  <v-app>
    <v-app-bar
      app
      color="secondary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Game Logo"
          class="shrink mr-2"
          contain
          src="https://www.spilnu.dk/cdn-cgi/image/format=auto,fit=scale-down,width=124/theme/Spilnu/img/sn/logo-menu.png"
          transition="scale-transition"
        />
      </div>

      <v-spacer></v-spacer>

      
        <span class="mr-2">By Malmos</span>
    </v-app-bar>

    <v-main> 
      <game-list></game-list>
    </v-main>
  </v-app>
</template>

<script>
import GameList from './components/GameList';

export default {
  name: 'App',

  components: {
    GameList
  },

  data: () => ({
    //
  }),
};
</script>
