# vuetify-datetime

This component works with vuetify. It uses v-text-field, v-date-picker and v-timer-picker.

- 14/05/2019 12:13
- 14/05/2019 12:13:14 (use seconds)
- Locale allows you to define other date formats.

v-model parent (milliseconds)
1557802800000

if you want a simple date component without time format, please, try this:
<p><a href="https://github.com/juareznasato/vuetify-date.git" target="_blank">vuetify-date</a></p>


## Features

- Vuetify dependency.
- moment dependency.
- Works fine with Chrome and Firefox. Others not tested.

## Links
<p><a href="https://v450e.codesandbox.io/">See DEMO here</a></p>
<p><a href="https://github.com/juareznasato/vuetify-datetime" target="_blank">GitHub</a></p>
<p><a href="https://www.npmjs.com/package/vuetify-datetime" target="_blank">npm</a></p>

## Usage

### Globally:
```
Install:
$ npm install vuetify-datetime --save

To upgrade to version 1.X.X you must remove version 0.X.X, before installing.
$ npm remove vuetify-datetime

Register component:
1- Create a src/modules/vuetify-datetime.js file with the following content:
import Vue from "vue";
import VuetifyDateTime from "vuetify-datetime";
Vue.use(VuetifyDateTime);
export default VuetifyDateTime;
2- Add to src/mains.js file:
import "./modules/vuetify-datetime.js";

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
      closeOnDateClick: false,  - You can define what happens after clicking the date picker: Close the window or go to the timer picker.
      useSeconds: false,        - Set true to working with seconds as well.
      clearable: true
    }
  })
};
</script>

```
### As component:
```
<template>
  <div>
    <VuetifyDateTime v-model="value" v-bind:label="label" v-bind:options="options"/>
    v-model parent: {{ value }}
  </div>
</template>
<script>
import VuetifyDateTime from "@/components/VuetifyDateTime.vue";
export default {
  components: {
    VuetifyDateTime
  },
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
      closeOnDateClick: false,  - You can define what happens after clicking the date picker: Close the window or go to the timer picker.
      useSeconds: false,        - Set true to working with seconds as well.
      clearable: true
    }
  })
};
</script>
```
