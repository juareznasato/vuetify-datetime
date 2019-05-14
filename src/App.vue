<template>
  <div id="app">
    <VuetifyDateTime v-model="value" v-bind:label="label" v-bind:config="config" />
    Parent v-model: {{ value }}
  </div>
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
      locale: "pt-BR",
      format: "DD/MM/YYYY",
      clearable: true
    }
  })
};
</script>
