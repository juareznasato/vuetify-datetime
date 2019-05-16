<template>
  <v-app id="inspire">
    <v-toolbar dark app fixed clipped-left color="cyan"></v-toolbar>
    <v-content>
      <VuetifyDateTime v-model="value" v-bind:label="label" v-bind:config="config" />
      Parent v-model: {{ value }}
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
    value: 1558043415000, //1557953700000, 16/05/2019 18:50:15
    label: "Data",
    config: {
      tabDateTitle: "Data", 
      tabTimeTitle: "Hora",
      locale: "pt-BR",
      format: "DD/MM/YYYY",
      icon: "event",
      closeOnDatePicker: false,
      useSeconds: false,
      clearable: true
    }
  })
};
</script>
