<template>
  <div>
    <!-- Application text -->
    <div class="application-text">
      <p>Thank you for choosing SWSI.</p>
    </div>

    <!-- Inputs -->
    <div class="input">
      <button class="new-appli-btn" @click="newApplication()">
        New Application
      </button>
      <input
        id="appNum"
        v-model="appNum"
        type="number"
        name="application-num"
        class="application-num"
        placeholder="Application Number"
      />
      <button class="continue-btn" @click="continueApplication()">
        Continue
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  data() {
    return {
      appNum: 0,
    }
  },
  methods: {
    newApplication() {
      this.$emit('customer-info')
    },
    async continueApplication() {
      const appNumUnknown = this.appNum as unknown
      const appNumString = appNumUnknown as string

      const url =
        'https://3498-180-190-48-16.ap.ngrok.io/applications/' + appNumString

      console.log(url)

      // const options = {
      //   headers: { 'content-type': 'application/json' },
      // }
      try {
        const res = await this.$axios.post(url)

        const resData = res.data
        console.log(resData)

        const stage = resData.applicationStage
        console.log(stage)

        this.$emit('set-app-num', this.appNum)

        // STEP 2
        if (stage === 'Uploading Requirements') {
          this.$emit('upload-reqs')
          // STEP 2A
        } else if (stage === 'Adding Representative') {
          this.$emit('rep-info')

          // STEP 3
        } else if (stage === 'Printing and Preparing Documents') {
          this.$emit('print-forms')
          // STEP 4
        } else if (stage === 'Pending Surveyor Visit') {
          this.$emit('schedule-visit')
        } else if (stage === 'Waiting for Survey Schedule') {
          this.$emit('schedule-visit')
        } // STEP 5
        else if (stage === 'Purchasing of Materials') {
          this.$emit('purchase-materials')
        }

        // STEP 6
        else if (stage === 'Pending Onsite Visit') {
          this.$emit('onsite-signing')

          // STEP 7
        } else if (stage === 'Pending Installation') {
          this.$emit('installation-activation')
        } else if (stage === 'Completed') {
          this.$emit('installation-activation')
        } else {
          console.log('Error')
        }
      } catch (err: any) {
        console.log(err)
      }
    },
  },
})
</script>

<style lang="postcss" scoped>
/* Application text */
.application-text {
  margin-top: 13%;
  text-align: center;
  font-family: 'Inter';
  font-style: normal;
  color: #000080;
  font-weight: 700;
  font-size: 250%;
}

/* Buttons */
.input {
  margin-top: 3%;
  margin-left: 15%;
}

.new-appli-btn {
  background: #000080;
  color: #ffffff;
  box-shadow: 0px 4px 10px 6px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  padding: 1% 5% 1% 5%;
  font-size: 140%;
  position: absolute;
  font-family: 'Inter';
  font-style: normal;
  font-weight: 800;
}

.application-num {
  margin-left: 30%;
  margin-right: 1%;
  background: #ffffff;
  box-shadow: 0px 4px 10px 5px rgba(0, 0, 0, 0.25);
  padding: 1% 5% 1% 2%;
  font-size: 140%;
  border-radius: 10px;
}

.continue-btn {
  background: #000080;
  color: #ffffff;
  box-shadow: 0px 4px 10px 6px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  padding: 1% 5% 1% 5%;
  font-size: 140%;
  position: absolute;
  font-family: 'Inter';
  font-style: normal;
  font-weight: 800;
}
</style>