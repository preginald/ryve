<template>
  <v-container>
    <v-row v-if="debug.show">
      <v-col class="mb-5" cols="12">
        <h2 class="headline font-weight-bold mb-3">{{ heading }}</h2>

        <ul>
          <li>TV size:{{ tvsize }}</li>
          <li>Mount surface:{{ mount_surface }}</li>
          <li>Mount type:{{ mount_type }}</li>
          <li>Mount recessed:{{ mount_recessed }}</li>
          <li>Conceal wires:{{ conceal_wires }}</li>
          <li>Concealable cables:{{ concealableCables }}</li>
        </ul>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "debug",
  props: ["data", "debug"],
  data: () => ({
    heading: "Debug",
  }),
};
</script>