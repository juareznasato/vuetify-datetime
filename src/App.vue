<template>
  <v-app id="inspire">
    <v-toolbar dark app fixed clipped-left color="cyan"></v-toolbar>
    <v-content>
      <VuetifyDateTime v-model="value1" v-bind:label="label1" v-bind:config="config1" />
      Parent v-model milliseconds: {{ value1 }}<br><br>
      <VuetifyDateTime v-model="value2" v-bind:label="label2" v-bind:config="config2" />
      Parent v-model milliseconds: {{ value2 }}<br><br>
      <VuetifyDateTime v-model="value3" v-bind:label="label3" v-bind:config="config3" />
      Parent v-model milliseconds: {{ value3 }}<br><br>
    </v-content>
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
    config1: {
      tabDateTitle: "Data", 
      tabTimeTitle: "Hora",
      locale: "pt-BR",
      format: "DD/MM/YYYY",
      icon: "event",
      iconTime: "",
      closeOnDateClick: false,
      useSeconds: false,
      clearable: false
    },
    value2: 1558220700000,
    label2: "Date Hora",
    config2: {
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
    config3: {
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
