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
    value: 1577239200000, //1557673468418, // 12/05/2019 12:04:28
    label: "Data",
    config: {
      tabDateTitle: "Data", 
      tabTimeTitle: "Hora",
      locale: "pt-BR",
      format: "DD/MM/YYYY",
      clearable: true
    }
  })
};
</script>
