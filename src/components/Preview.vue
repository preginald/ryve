<template>
  <v-container>
    <v-row>
      <v-col class="mb-5" cols="12">
        <h2 class="headline font-weight-bold mb-3">{{ heading }}</h2>
        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">Code</th>
                <th class="text-left">Type</th>
                <th class="text-left">Item</th>
                <th class="text-right">Qty</th>
                <th class="text-right">$</th>
                <th class="text-right">Total</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in items" :key="item.name">
                <td>{{ item.code }}</td>
                <td>
                  <v-chip
                    small
                    label
                    text-color="white"
                    :color="chipColour(item.type)"
                    >{{ item.type }}</v-chip
                  >
                </td>
                <td>{{ item.name }}</td>
                <td class="text-right">{{ item.qty }}</td>
                <td class="text-right">{{ item.price }}</td>
                <td class="text-right">{{ item.lineTotal }}</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-col>
    </v-row>
    <v-row v-if="debug">
      <v-col class="mb-5" cols="12">
        <h2 class="headline font-weight-bold mb-3">Debug</h2>

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
  name: "preview",
  props: ["items"],
  data: () => ({
    heading: "Preview",
  }),
  methods: {
    chipColour(type) {
      let colour = "blue";
      switch (type) {
        case "labour":
          colour = "blue";
          break;
        case "item":
          colour = "purple";
          break;
      }
      return colour;
    },
  },
};
</script>