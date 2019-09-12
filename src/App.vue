<template>
  <v-app id="inspire">
    <v-card-title>
      <v-toolbar flat class="elevation-2" color="cyan">
        <v-toolbar-title>vuetify-datetime</v-toolbar-title>
      </v-toolbar>
    </v-card-title>
    <v-card-text>
      <v-container>
        <v-row>
          <v-col cols="4" sm="4" md="4">
            <VuetifyDateTime v-model="value1" v-bind:label="label1" v-bind:options="options1" />
            Parent v-model milliseconds: {{ value1 }}
          </v-col>
          <br />
          <br />
          <v-col cols="4" sm="4" md="4">
            <VuetifyDateTime v-model="value2" v-bind:label="label2" v-bind:options="options2" />
            Parent v-model milliseconds: {{ value2 }}
          </v-col>
          <br />
          <br />
          <v-col cols="4" sm="4" md="4">
            <VuetifyDateTime v-model="value3" v-bind:label="label3" v-bind:options="options3" />
            Parent v-model milliseconds: {{ value3 }}
          </v-col>
          <br />
          <br />
        </v-row>
      </v-container>
    </v-card-text>
  </v-app>
</template>

<script>
import VuetifyDateTime from "./components/VuetifyDateTime.vue";

export default {
  name: "app",
  components: {
    VuetifyDateTime
  },
  data: () => ({
    value1: 1558220700000,
    label1: "Data Hora",
    options1: {
      tabDateTitle: "Data",
      tabTimeTitle: "Hora",
      locale: "pt-BR",
      format: "DD/MM/YYYY",
      icon: "event",
      iconTime: "",
      backgroundColor: "blue",
      closeOnDateClick: false,
      useSeconds: false,
      clearable: false
    },
    value2: 1558220700000,
    label2: "Date Hora",
    options2: {
      tabDateTitle: "Data",
      tabTimeTitle: "Hora",
      locale: "pt-BR",
      format: "DD/MM/YYYY",
      icon: "",
      iconTime: "av_timer",
      closeOnDateClick: true,
      useSeconds: false,
      clearable: false
    },
    value3: 1558220710000,
    label3: "Date Time",
    options3: {
      tabDateTitle: "Date",
      tabTimeTitle: "Time",
      locale: "en-US",
      format: "YYYY-MM-DD",
      icon: "event",
      iconTime: "",
      closeOnDateClick: false,
      useSeconds: true,
      clearable: true
    }
  })
};
</script>
