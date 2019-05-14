# vuetify-money

This component works with v-text-field (vuetify).

v-text-field
14/05/2019 12:13:14 or others formats.

v-model parent (millisecond)
1557802800000

## Features

- Vuetify Dependency
- Works fine with Chrome and Firefox. Others not tested.

## Usage:

### Globally
```
Install:
$ npm install vuetify-datetime --save

Register component:
import Vue from "vue";
import VuetifyDateTime from "vuetify-datetime";
Vue.use(VuetifyDateTime);
export default VuetifyDateTime;

Parent component:
<template>
  <div>
    <VuetifyDateTime v-model="value" v-bind:label="label" v-bind:config="config"/>
    v-model parent: {{ value }}
  </div>
</template>
<script>
export default {
  data: () => ({
    value: "1557802800000",
    label: "Date",
    config: {
      locale: "pt-BR",
      format: "DD/MM/YYYY",
      clearable: true
    }
  })
};
</script>

```
### As component
```
<template>
  <div>
    <VuetifyDateTime v-model="value" v-bind:label="label" v-bind:config="config"/>
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
    config: {
      locale: "pt-BR",
      format: "DD/MM/YYYY",
      clearable: true
    }
  })
};
</script>
```
