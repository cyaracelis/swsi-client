<template>
  <li>{{ name }}</li>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    name: {
      required: true,
      type: String,
    },
  },
})
</script>

<style lang="postcss" scoped>
li {
  padding-top: 2%;
  font-size: 120%;
  font-family: Inter;
}
</style>