<template>
  <v-app>
    <v-app-bar
      app
      color="white"
      light
    >
      <div class="d-flex align-center">
        <v-img
          alt="Ryve Logo"
          class="shrink mr-2"
          contain
          src="https://www.ryve.com.au/wp-content/uploads/2020/05/Ryve-Logo-Web-1.png"
          transition="scale-transition"
          width="100"
        />

    </v-app-bar>

    <v-main>
      <Form/>
    </v-main>
  </v-app>
</template>

<script>
import Form from "./components/Form";

export default {
  name: "App",

  components: {
    Form,
  },

  data: () => ({
    //
  }),
};
</script>
