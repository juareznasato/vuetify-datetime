<template>
  <div>
    <v-layout row>
      <v-flex xs12 sm6 md4>
        <v-menu
          v-model="menu"
          v-bind:close-on-content-click="false"
          v-bind:nudge-right="40"
          lazy
          transition="scale-transition"
          offset-y
          data-app="true"
        >
          <v-text-field
            v-model="compShow"
            v-bind:readonly="readonly"
            v-bind:clearable="config.clearable"
            v-bind:label="label"
            slot="activator"
            prepend-icon="event"
          ></v-text-field>


          <v-tabs color="grey lighten-2" slider-color="cyan" v-model="activeTab">
            <v-tab v-bind:key="0" ripple>{{ config.tabDateTitle }}</v-tab>
            <v-tab v-bind:key="1" ripple>{{ config.tabTimeTitle }}</v-tab>
            <v-tabs-items>
              <v-tab-item v-bind:key="0">
                <v-card flat style="overflow: auto">
                  <v-date-picker
                    v-model="modDate"
                    v-on:input="(menu = false), emit()"
                    v-bind:locale="config.locale"
                    no-title
                  ></v-date-picker>
                </v-card>
              </v-tab-item>
              <v-tab-item v-bind:key="1">
                <v-card flat>
                  <v-time-picker v-model="time" @change="menuTime = false" format="24hr" landscape></v-time-picker>
                </v-card>
              </v-tab-item>
            </v-tabs-items>
          </v-tabs>



        </v-menu>
      </v-flex>
    </v-layout>
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
        return { tabDateTitle: "Data", tabTimeTitle: "Hora", locale: "pt-BR", format: "DD/MM/YYYY", clearable: false };
      }
    }
  },
  data: () => ({
    modDate: "",
    modDateFormatted: "",
    time: "00:00:00",
    menu: false,
    readonly: true,
    activeTab: 0
  }),
  computed: {
    compShow: {
      get: function() {
        const THIS = this;
        return this.value
          ? (THIS.modDateFormatted = moment(new Date(this.value)).format(
              this.config.format
            ))
          : null;
      },
      set: function() {
        const THIS = this;
        THIS.modDate = null;
        THIS.modDateFormatted = null;
        this.$emit("input", null);
      }
    }
  },
  watch: {
    // When computed.compShow.modDateFormatted is changed:
    modDateFormatted() {
      return this.value
        ? (this.modDate = moment(new Date(this.value)).format("YYYY-MM-DD"))
        : null;
    }
  },
  methods: {
    emit() {
      this.$emit("input", this.stringToMillisecond(this.modDate, this.time));
    },
    stringToMillisecond: function(date, time) {
      return Date.parse(date + " " + time);
    }
  }
};
// Str to milli
// var d = Date.parse(date);
// milli to date
// this.date = new Date(d);
</script>
