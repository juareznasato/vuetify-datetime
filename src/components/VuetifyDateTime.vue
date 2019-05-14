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
          full-width
          max-width="290"
          min-width="290px"
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
          <v-date-picker
            v-model="modDate"
            v-on:input="(menu = false), emit()"
            v-bind:locale="config.locale"
            no-title
          ></v-date-picker>
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
        return { locale: "pt-BR", format: "DD/MM/YYYY", clearable: false };
      }
    }
  },
  data: () => ({
    modDate: "",
    modDateFormatted: "",
    time: "00:00:00",
    menu: false,
    readonly: true
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
