# vuetify-datetime

This component works with vuetify.
input:
- 14/05/2019 12:13    (Locale allows you to define others date formats).
- 14/05/2019 12:13:14 (with seconds)

v-model: (milliseconds)
1557802800000

if you want a simple date component without time format, please, try this:
<p><a href="https://github.com/juareznasato/vuetify-date.git" target="_blank">vuetify-date</a></p>

## Dependency
- VueJS
- Vuetify 2.x
- moment

## Links
<p><a href="https://v450e.codesandbox.io/">See DEMO here</a></p>
<p><a href="https://github.com/juareznasato/vuetify-datetime" target="_blank">GitHub</a></p>
<p><a href="https://www.npmjs.com/package/vuetify-datetime" target="_blank">npm</a></p>

## Install:
```
$ npm install vuetify-datetime --save

Register component:
1- Create a src/plugins/vuetify-datetime.js file with the following content:
import Vue from "vue";
import VuetifyDateTime from "vuetify-datetime";
Vue.use(VuetifyDateTime);
export default VuetifyDateTime;

2- Add to src/mains.js file:
import "./plugins/vuetify-datetime.js";

Parent component:
<template>
  <div>
    <vuetify-datetime v-model="value" v-bind:label="label" v-bind:options="options"/>
    v-model parent: {{ value }}
  </div>
</template>
<script>
export default {
  data: () => ({
    value: "1557802800000",
    label: "Date",
    options: {
      tabDateTitle: "Data",
      tabTimeTitle: "Hora",
      locale: "pt-BR",
      format: "DD/MM/YYYY",     - Date format only. Do not include the time format here.
      icon: "event",            - "" to disable.
      iconTime: "av_timer",     - "" to disable. Clicking on this icon, will open the time window.
      backgroundColor: "blue",
      closeOnDateClick: false,  - You can define what happens after clicking the date picker: Close the window or go to the timer picker.
      useSeconds: false,        - Set true to working with seconds as well.
      clearable: true
    }
  })
};
</script>
