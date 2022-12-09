<template>
  <div class="body-cover">
    <!-- Header -->
    <nav-bar />
    <application-landing-menu
      v-if="show.landing"
      @set-app-num="(appNum) => setAppNum(appNum)"
      @customer-info="handleApplication('customer_info', 'landing')"
      @upload-reqs="handleApplication('upload_reqs', 'landing')"
      @rep-info="handleApplication('rep_info', 'landing')"
      @print-forms="handleApplication('print_forms', 'landing')"
      @schedule-visit="handleApplication('schedule_visit', 'landing')"
      @purchase-materials="handleApplication('purchase_materials', 'landing')"
      @onsite-signing="handleApplication('onsite_signing', 'landing')"
      @installation-activation="
        handleApplication('installation_activation', 'landing')
      "
    />
    <application-customer-info
      v-if="show.customer_info"
      :app-num="appNum"
      @set-app-num="(appNum) => setAppNum(appNum)"
      @upload-reqs="handleApplication('upload_reqs', 'customer_info')"
    />
    <application-upload-reqs
      v-if="show.upload_reqs"
      :app-num="appNum"
      @rep-info="handleApplication('rep_info', 'upload_reqs')"
      @print-forms="handleApplication('print_forms', 'upload_reqs')"
    />
    <application-rep-info
      v-if="show.rep_info"
      :app-num="appNum"
      @print-forms="handleApplication('print_forms', 'rep_info')"
    />
    <application-print-forms
      v-if="show.print_forms"
      :app-num="appNum"
      @schedule-visit="handleApplication('schedule_visit', 'print_forms')"
    />
    <application-schedule-visit
      v-if="show.schedule_visit"
      :app-num="appNum"
      @purchase-materials="
        handleApplication('purchase_materials', 'schedule_visit')
      "
    />
    <application-purchase-materials
      v-if="show.purchase_materials"
      :app-num="appNum"
      @onsite-signing="
        handleApplication('onsite_signing', 'purchase_materials')
      "
    />

    <application-onsite-signing
      v-if="show.onsite_signing"
      :app-num="appNum"
      @installation-activation="
        handleApplication('installation-activation', 'onsite-signing')
      "
    />

    <application-installation-activation
      v-if="show.installation_activation"
      :app-num="appNum"
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
      appNum: 0,
    }
  },

  methods: {
    handleApplication(newStep: string, currStep: string) {
      this.$set(this.show, newStep, true)
      this.$set(this.show, currStep, false)
    },

    setAppNum(appNum: Number) {
      this.$set(this, 'appNum', appNum)
      try {
        console.log(appNum)
        console.log(this.appNum)
      } catch (err: any) {
        console.log('Not a number')
      }
      console.log('Is it working? yes')
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