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
      <v-spacer></v-spacer>
      <v-btn text to="/">Home</v-btn>
      <v-btn text to="/test">Test</v-btn>
      <v-btn text to="/about">About</v-btn>
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
    <v-footer>
      <v-col class="text-right" cols="2"> </v-col>
      <v-col class="text-center" cols="8">
        {{ new Date().getFullYear() }} —
        <strong>Peter Reginald for RYVE</strong>
      </v-col>
      <v-col class="text-right" cols="2">
        <a href="https://github.com/preginald/ryve">Code</a>
      </v-col>
    </v-footer>
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
