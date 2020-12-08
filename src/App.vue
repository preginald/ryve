<template>
  <v-app>
    <v-app-bar app>
      <v-img
        alt="Ryve Logo"
        class="shrink mr-2"
        contain
        src="https://www.ryve.com.au/wp-content/uploads/2020/05/Ryve-Logo-Web-1.png"
        transition="scale-transition"
        width="100"
      />
      <v-btn text>
        <router-link to="/">Home</router-link>
      </v-btn>
      <v-btn text>
        <router-link to="/about">About</router-link>
      </v-btn>
      <v-spacer></v-spacer>
      <v-switch
        v-model="$vuetify.theme.dark"
        :label="$vuetify.theme.dark ? 'Dark' : 'Light'"
        hide-details
      ></v-switch>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    //
  }),
};
</script>
