<template>
  <div>
    <v-layout row>
      <v-flex xs12 sm6 md4>
        <v-menu
          v-model="menu"
          v-bind:close-on-content-click="false"
          v-bind:nudge-right="40"
          transition="scale-transition"
          data-app="true"
          offset-y
          lazy
        >
          <v-text-field
            v-model="compShow"
            v-bind:readonly="readonly"
            v-bind:clearable="options.clearable"
            v-bind:label="label"
            v-bind:prepend-icon="options.icon"
            slot="activator"
          ></v-text-field>
          <v-tabs color="grey lighten-2" slider-color="cyan" v-model="activeTab">
            <v-tab v-bind:key="0" ripple>{{ options.tabDateTitle }}</v-tab>
            <v-tab v-bind:key="1" ripple>{{ options.tabTimeTitle }}</v-tab>
            <v-tabs-items>
              <v-tab-item v-bind:key="0">
                <v-card flat style="overflow: auto">
                  <v-date-picker
                    v-model="modDate"
                    v-on:change="closingControl(), emit()"
                    v-bind:locale="options.locale"
                    no-title
                  ></v-date-picker>
                </v-card>
              </v-tab-item>
              <v-tab-item v-bind:key="1">
                <v-card flat>
                  <v-time-picker
                    ref="refTimePicker"
                    v-model="modTime"
                    v-on:change="(menu = false), emit()"
                    format="24hr"
                    landscape
                  ></v-time-picker>
                </v-card>
              </v-tab-item>
            </v-tabs-items>
          </v-tabs>
        </v-menu>
      </v-flex>
    </v-layout>
    formattedDate {{ formattedDate }}
    <br>
    modDate {{ modDate }}
    <br>
    modTime {{ modTime }}
    <br>
    menu {{ menu }}
  </div>
</template>

<script>
import moment from "moment";

export default {
  model: { prop: "value", event: "input" },
  props: {
    value: {
      type: [Number, String],
      default: 0
    },
    label: {
      type: String,
      default: "Label"
    },
    options: {
      type: Object,
      default: function() {
        return {
          tabDateTitle: "Data",
          tabTimeTitle: "Hora",
          locale: "pt-BR",
          format: "DD/MM/YYYY",
          icon: "event",
          closeOnDatePicker: false,
          clearable: false
        };
      }
    }
  },
  data: () => ({
    modDate: "",
    modTime: "00:00",
    formattedDate: "",
    menu: false,
    readonly: true,
    activeTab: 0
  }),
  computed: {
    compShow: {
      get: function() {
        const THIS = this;
        let mdf = this.value
          ? (THIS.formattedDate = moment(new Date(this.value)).format(
              this.options.format
            ))
          : "";
        let mt = this.value
          ? (THIS.modTime = moment(new Date(this.value)).format("HH:mm"))
          : "";
        return mdf + " " + mt;
      },
      set: function() {
        const THIS = this;
        THIS.modDate = null;
        THIS.modTime = "00:00";
        THIS.formattedDate = null;
        this.$emit("input", null);
      }
    }
  },
  watch: {
    // When computed.compShow.formattedDate is changed:
    formattedDate() {
      return this.value
        ? (this.modDate = moment(new Date(this.value)).format("YYYY-MM-DD"))
        : null;
    },
    // Open always on date tab and selected hour
    menu() {
      if (!this.menu) {
        this.activeTab = 0;
        this.$refs.refTimePicker.selectingHour = true
      }
    }
  },
  methods: {
    emit() {
      this.$emit("input", this.stringToMillisecond(this.modDate, this.modTime));
    },
    stringToMillisecond: function(date, time) {
      return Date.parse(date + " " + time);
    },
    closingControl() {
      if (this.options.closeOnDatePicker === true) {
        this.menu = false;
      } else {
        this.activeTab = 1;
      }
    }
  }
};
// Str to milli
// var d = Date.parse(date);
// milli to date
// this.date = new Date(d);
</script>
