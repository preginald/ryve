<template>
  <v-container>
    <v-row>
      <v-col cols="12" md="2">
        <v-switch label="form" v-model="form"></v-switch>
      </v-col>
      <v-col cols="12" md="2">
        <v-switch label="buttons" v-model="buttons"></v-switch>
      </v-col>
    </v-row>
    <v-row>
      <v-col class="mb-5" cols="12">
        <h2 class="headline font-weight-bold mb-3">
          {{ heading }}
        </h2>
        <v-row>
          <v-form>
            <v-container>
              <h4 class="headline font-weight-bold mb-3">1. TV Size</h4>
              <v-row v-if="form">
                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="tvsize_cm"
                    type="number"
                    label="TV Size (cm)"
                    @keyup="tvsize('cm')"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="tvsize_inch"
                    type="number"
                    label="TV Size (inch)"
                    @keyup="tvsize('inch')"
                  ></v-text-field>
                </v-col>
              </v-row>
              <v-row v-if="buttons">
                <v-col cols="12" md="12">
                  <v-btn-toggle mandatory v-model="tv_size_toggle">
                    <v-btn color="primary">Medium</v-btn>
                    <v-btn color="primary">Large</v-btn>
                    <v-btn color="primary">X-Large</v-btn>
                  </v-btn-toggle>
                </v-col>
              </v-row>
            </v-container>
            <v-container v-if="tvsize_cm">
              <h4 class="headline font-weight-bold mb-3">2. Mounting</h4>
              <v-row v-if="form">
                <v-col cols="12" md="6">
                  <v-radio-group
                    v-model="mount_type"
                    mandatory
                    @change="mountType"
                  >
                    <v-radio label="None" value="none"></v-radio>
                    <v-radio label="Stand" value="stand"></v-radio>
                    <v-radio label="Wall mount" value="wall"></v-radio>
                  </v-radio-group>
                </v-col>
              </v-row>
              <v-row v-if="buttons">
                <v-col cols="12" md="12">
                  <v-btn-toggle mandatory v-model="mount_type_toggle">
                    <v-btn color="primary">None</v-btn>
                    <v-btn color="primary">Stand</v-btn>
                    <v-btn color="primary">Wall</v-btn>
                  </v-btn-toggle>
                </v-col>
              </v-row>
            </v-container>
            <v-container v-if="mount_type == 'wall'">
              <h4 class="headline font-weight-bold mb-3">
                3. Mounting surface
              </h4>
              <v-row v-if="form">
                <v-col cols="12" md="6">
                  <v-select
                    @change="mountSurface"
                    v-model="mount_surface"
                    :items="mount_surfaces"
                    label="Mount surface"
                  ></v-select>
                </v-col>
              </v-row>
              <v-row v-if="buttons">
                <v-col cols="12" md="12">
                  <v-btn-toggle mandatory v-model="mount_surface_toggle">
                    <v-btn color="primary">Plaster</v-btn>
                    <v-btn color="primary">Brick</v-btn>
                    <v-btn color="primary">Concrete</v-btn>
                  </v-btn-toggle>
                </v-col>
              </v-row>
            </v-container>
            <v-container v-if="mount_type == 'wall'">
              <h4 class="headline font-weight-bold mb-3">
                4. Mounting options
              </h4>
              <v-row v-if="mount_type == 'wall' && form">
                <v-col v-if="mount_surface == 'plaster'" cols="12" md="3">
                  <v-checkbox
                    @change="mountRecessed"
                    v-model="mount_recessed"
                    label="Recessed"
                  ></v-checkbox>
                </v-col>
                <v-col
                  v-if="mount_type == 'wall' && mount_surface"
                  cols="12"
                  md="3"
                >
                  <v-checkbox
                    @change="aboveFireplace"
                    v-model="mount_fireplace"
                    label="Above fireplace"
                  ></v-checkbox>
                </v-col>
                <v-col v-if="mount_surface" cols="12" md="3">
                  <v-checkbox
                    @change="concealCables"
                    v-model="conceal_cables"
                    label="Conceal cables"
                  ></v-checkbox>
                </v-col>
                <v-col v-if="mount_type == 'wall'" cols="12" md="3">
                  <v-checkbox
                    @change="toggleByoWallMount"
                    v-model="mount_supplied"
                    label="BYO mount"
                  ></v-checkbox>
                </v-col>
              </v-row>
              <v-row v-if="buttons">
                <v-col v-if="mount_surface == 'plaster'">
                  <v-btn
                    @click="toggleButton('mount_recessed')"
                    :color="mount_recessed ? 'primary' : 'grey'"
                    >Recessed</v-btn
                  >
                </v-col>
                <v-col>
                  <v-btn
                    @click="toggleButton('mount_fireplace')"
                    :color="mount_fireplace ? 'primary' : 'grey'"
                    >Above fireplace</v-btn
                  >
                </v-col>
                <v-col>
                  <v-btn
                    @click="toggleButton('conceal_cables')"
                    :color="conceal_cables ? 'primary' : 'grey'"
                    >Conceal cables</v-btn
                  >
                </v-col>
                <v-col>
                  <v-btn
                    @click="toggleButton('mount_supplied')"
                    :color="mount_supplied ? 'primary' : 'grey'"
                    >BYO mount</v-btn
                  >
                </v-col>
              </v-row>
            </v-container>
          </v-form>
        </v-row>
      </v-col>
    </v-row>
    <Preview :items="items" />
  </v-container>
</template>

<script>
import Preview from "./Preview.vue";

export default {
  name: "Form",
  components: {
    Preview,
  },
  data: () => ({
    heading: "TV Installation",
    form: true,
    buttons: false,
    labour: 100,
    tvsize_cm: 0,
    tvsize_inch: 0,
    mount_surfaces: ["brick", "concrete", "plaster"],
    mount_surface: "",
    mount_type_toggle: "",
    mount_surface_toggle: "",
    tv_size_toggle: "",
    mount_type: "none",
    conceal_cables: false,
    mount_supplied: false,
    mount_recessed: false,
    mount_fireplace: false,
    datapoints: 0,
    objIndex: 0,
    items: [],
    debug: {},
  }),
  computed: {},
  watch: {
    form: function () {
      if (!this.form && !this.buttons) {
        this.buttons = true;
      }
    },
    buttons: function () {
      if (!this.buttons && !this.form) {
        this.form = true;
      }
    },
    tv_size_toggle: function (val) {
      switch (val) {
        case 0:
          this.tvsize_inch = 50;
          break;
        case 1:
          this.tvsize_inch = 70;
          break;
        case 2:
          this.tvsize_inch = 90;
          break;
      }
      this.tvsize("inch");
    },
    mount_type_toggle: function (val) {
      switch (val) {
        case 0:
          this.mount_type = "none";
          break;
        case 1:
          this.mount_type = "stand";
          break;
        case 2:
          this.mount_type = "wall";
          break;
      }
      this.mountType();
    },
    mount_surface_toggle: function (val) {
      switch (val) {
        case 0:
          this.mount_surface = "plaster";
          break;
        case 1:
          this.mount_surface = "brick";
          break;
        case 2:
          this.mount_surface = "concrete";
          break;
      }
      this.mountSurface();
    },
  },
  methods: {
    addLineItem(code, name, type, qty, price) {
      let b = {};
      b.code = code;
      b.name = name;
      b.qty = qty;
      b.price = price;
      b.type = type;
      b.lineTotal = qty * price;
      this.items.push(b);
    },
    lineItemIndex(code) {
      return this.items.findIndex((obj) => obj.code === code);
    },
    lineItemExists(code) {
      return this.lineItemIndex(code) > -1 ? true : false;
    },
    removeLineItem(code) {
      let objIndex = this.lineItemIndex(code);
      if (objIndex > -1) {
        this.items.splice(objIndex, 1);
      }
    },
    cmToInch: function () {
      this.tvsize_inch = this.tvsize_cm * 0.393701;
    },
    inchToCm: function () {
      this.tvsize_cm = this.tvsize_inch * 2.54;
    },
    tvsize(unit) {
      if (unit == "cm") {
        this.cmToInch();
      } else {
        this.inchToCm();
      }
      this.removeLineItem("tvwallmount");
      this.removeLineItem("minimumbooking");
      this.mountType();
      this.addLineItem(
        "minimumbooking",
        "Minimum callout",
        "labour",
        1,
        this.labour
      );
    },
    mountType: function () {
      let code = "mounttype";
      this.removeLineItem(code);
      this.clearWallMount();
      switch (this.mount_type) {
        case "wall":
          this.addLineItem(code, "Wall mount", "labour", 1, this.labour);
          this.addLineItem("hdmicable", "5m HDMI cable", "item", 1, 20);
          this.wallMountType();
          break;
        case "stand":
          this.addLineItem(code, "TV stand", "labour", 0.25, this.labour);
          this.addLineItem("hdmicable", "2m HDMI cable", "item", 1, 10);
          break;
        case "none":
          this.addLineItem(code, "Setup only", "labour", 0.5, this.labour);
          break;

        default:
          break;
      }
    },
    mountSurface: function () {
      let code = "mountsurface";
      this.removeLineItem(code);
      switch (this.mount_surface) {
        case "plaster":
          this.addLineItem(
            code,
            "Standard mount on plaster wall",
            "labour",
            1,
            this.labour
          );
          break;
        case "brick":
          this.mount_recessed = false;
          this.mountRecessed();
          this.concealCables();
          this.addLineItem(
            code,
            "Standard mount on brick wall",
            "labour",
            2,
            this.labour
          );
          break;
        case "concrete":
          this.mount_recessed = false;
          this.mountRecessed();
          this.concealCables();
          this.addLineItem(
            code,
            "Standard mount on concrete wall",
            "labour",
            3,
            this.labour
          );
          break;
      }
    },
    mountRecessed: function () {
      let code = "mountrecessed";
      if (this.mount_recessed && !this.lineItemExists(code)) {
        this.addLineItem(code, "Recessed mount", "labour", 1, this.labour);
      }
      if (!this.mount_recessed) {
        this.removeLineItem(code);
      }
    },
    aboveFireplace: function () {
      let code = "mountfireplace";
      if (this.mount_fireplace && !this.lineItemExists(code)) {
        this.addLineItem(code, "Fireplace", "labour", 2, this.labour);
      }
      if (!this.mount_fireplace) {
        this.removeLineItem(code);
      }
    },
    concealCables: function () {
      let code = "concealcables";
      this.removeLineItem("concealconduit");
      this.removeLineItem(code);
      if (this.conceal_cables && this.mount_surface == "plaster") {
        this.addLineItem(code, "Conceal cables", "labour", 1, this.labour);
        this.addLineItem(
          "concealconduit",
          "TV cable conceal kit with 2 wall plates",
          "item",
          1,
          55
        );
      } else if (this.conceal_cables && this.mount_surface == "brick") {
        this.addLineItem(code, "Conceal cables", "labour", 0.5, this.labour);
        this.addLineItem(
          "concealconduit",
          "TV wall drop adhesive cable cover",
          "item",
          1,
          35
        );
      }
    },
    wallMountType: function () {
      let code = "tvwallmount";
      if (this.tvsize_inch < 40) {
        this.addLineItem(code, "Medium duty fixed wall mount", "item", 1, 150);
      } else if (this.tvsize_inch >= 40 && this.tvsize_inch < 70) {
        this.addLineItem(code, "Heavy duty fixed wall mount", "item", 1, 250);
      } else {
        this.addLineItem(
          code,
          "Extra Heavy duty fixed wall mount",
          "item",
          1,
          400
        );
      }
    },
    toggleByoWallMount: function () {
      if (this.mount_supplied) {
        this.removeLineItem("tvwallmount");
      } else {
        this.mountRecessed();
        this.wallMountType();
        this.aboveFireplace();
      }
    },
    clearWallMount: function () {
      this.removeLineItem("tvwallmount");
      this.removeLineItem("mountsurface");
      this.removeLineItem("concealcables");
      this.removeLineItem("concealconduit");
      this.removeLineItem("hdmicable");
    },
    toggleButton(option) {
      switch (option) {
        case "mount_recessed":
          this.mount_recessed = !this.mount_recessed;
          this.mountRecessed();
          break;
        case "mount_fireplace":
          this.mount_fireplace = !this.mount_fireplace;
          this.aboveFireplace();
          break;
        case "conceal_cables":
          this.conceal_cables = !this.conceal_cables;
          this.concealCables();
          break;
        case "mount_supplied":
          this.mount_supplied = !this.mount_supplied;
          this.toggleByoWallMount();
          break;
        default:
          break;
      }
    },
  },
};
</script>