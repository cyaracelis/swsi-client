<template>
  <div class="body-cover">
    <!-- Header -->
    <nav-bar />
    <application-landing-menu
      v-if="show.landing"
      @customer-info="handleApplication('customer_info', 'landing')"
    />
    <application-customer-info
      v-if="show.customer_info"
      @upload-reqs="handleApplication('upload_reqs', 'customer_info')"
    />
    <application-upload-reqs
      v-if="show.upload_reqs"
      @rep-info="handleApplication('rep_info', 'upload_reqs')"
      @print-forms="handleApplication('print_forms', 'upload_reqs')"
    />
    <application-rep-info
      v-if="show.rep_info"
      @print-forms="handleApplication('print_forms', 'rep_info')"
    />
    <application-print-forms
      v-if="show.print_forms"
      @schedule-visit="handleApplication('schedule_visit', 'print_forms')"
    />
    <application-schedule-visit
      v-if="show.schedule_visit"
      @purchase-materials="
        handleApplication('purchase_materials', 'schedule_visit')
      "
    />
    <application-purchase-materials
      v-if="show.purchase_materials"
      @onsite-signing="
        handleApplication('onsite_signing', 'purchase_materials')
      "
    />
    <application-onsite-signing
      v-if="show.onsite_signing"
      @installation-activation="
        handleApplication('installation-activation', 'onsite-signing')
      "
    />
    <application-installation-activation
      v-if="show.purchase_materials"
      @completed="$router.push('/')"
    />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  data() {
    return {
      show: {
        landing: true,
        customer_info: false,
        upload_reqs: false,
        rep_info: false,
        print_forms: false,
        schedule_visit: false,
        purchase_materials: false,
        onsite_signing: false,
        installation_activation: false,
      },
    }
  },

  methods: {
    handleApplication(newStep: string, currStep: string) {
      this.$set(this.show, newStep, true)
      this.$set(this.show, currStep, false)
    },
  },
})
</script>

<style lang="postcss" scoped>
/* Background */
.body-cover {
  background-size: cover;
  height: 100vh;
  overflow: scroll;
  background-image: url('~/assets/img/application_bg.png');
}
</style>