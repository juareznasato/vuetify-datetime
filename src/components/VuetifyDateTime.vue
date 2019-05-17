<template>
  <div>
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
        v-bind:clearable="config.clearable"
        v-bind:label="label"
        v-bind:prepend-icon="config.icon"
        v-bind:append-icon="config.iconTime"
        v-on:click:append="menu=true, activeTab=1"
        v-on:click:clear="menu=false"
        slot="activator"
      ></v-text-field>
      <v-tabs color="grey lighten-2" slider-color="cyan" v-model="activeTab">
        <v-tab v-bind:key="0" ripple>{{ config.tabDateTitle }}</v-tab>
        <v-tab v-bind:key="1" ripple>{{ config.tabTimeTitle }}</v-tab>
        <v-tabs-items>
          <v-tab-item v-bind:key="0">
            <v-card flat style="overflow: auto">
              <v-date-picker
                v-model="modDate"
                v-on:change="closingControl(), emit()"
                v-bind:locale="config.locale"
                no-title
              ></v-date-picker>
            </v-card>
          </v-tab-item>
          <v-tab-item v-bind:key="1">
            <v-card flat>
              <v-time-picker
                ref="refTimePicker"
                v-model="modTime"
                v-bind:use-seconds="config.useSeconds"
                v-on:change="(menu = false), emit()"
                format="24hr"
                landscape
                v-if="formattedDate !== null && formattedDate !== '' "
              ></v-time-picker>
            </v-card>
          </v-tab-item>
        </v-tabs-items>
      </v-tabs>
    </v-menu>
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
    config: {
      type: Object,
      default: function() {
        return {
          tabDateTitle: "Data",
          tabTimeTitle: "Hora",
          locale: "pt-BR",
          format: "DD/MM/YYYY",
          icon: "event",
          iconTime: "av_timer",
          closeOnDateClick: false,
          useSeconds: false,
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
              this.config.format
            ))
          : "";
        let mt = this.value
          ? (THIS.modTime = moment(new Date(this.value)).format(
              this.config.useSeconds ? "HH:mm:ss" : "HH:mm"
            ))
          : "";
        return mdf + " " + mt;
      },
      set: function() {
        const THIS = this;
        THIS.modDate = null;
        THIS.modTime = this.config.useSeconds ? "00:00:00" : "00:00";
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
        if (this.$refs.refTimePicker) {
          this.$refs.refTimePicker.selectingHour = true;
        }
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
      if (this.config.closeOnDateClick === true) {
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
