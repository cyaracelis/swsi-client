<template>
  <!-- New application text -->
  <div class="container">
    <div class="welcome">
      <p>
        <strong>Your application number is {{ appNum }}.</strong>
      </p>
    </div>

    <!-- Stepper temp -->
    <img src="~/assets/img/stepper_schedule_visit.png" class="stepper" />

    <!-- Schedule Information -->
    <div class="panel">
      <div class="schedule-details">
        <div class="left">
          <img src="~/assets/img/calendar.png" class="schedule-icon" />
        </div>
        <div class="right">
          <div class="schedule-header">
            <b>{{ displayHeading }}</b>
          </div>
          <div class="schedule-sub">
            {{ displaySub }}
          </div>
        </div>
      </div>

      <div class="gray-btn-center">
        <button class="gray-btn">
          Please wait for further instructions. <br />Thank you!
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    appNum: {
      type: Number,
      required: true,
    },
  },

  data() {
    return {
      displayHeading: '',
      displaySub: '',
      visitationSchedule: '0000',
    }
  },
  mounted() {
    this.getStatus()
  },
  methods: {
    nextStep() {
      this.$emit('purchase-materials')
    },

    async getVisit() {
      const appNumUnknown = this.appNum as unknown
      const appNumString = appNumUnknown as string

      const url =
        'https://3498-180-190-48-16.ap.ngrok.io/applications/step4/' +
        appNumString

      const response = await this.$axios.post(url)
      const resData = response.data
      const schedule = resData.visitationSchedule as string
      console.log(schedule)
      this.visitationSchedule = schedule
    },

    async getStatus() {
      const appNumUnknown = this.appNum as unknown
      const appNumString = appNumUnknown as string

      const url =
        'https://3498-180-190-48-16.ap.ngrok.io/applications/' + appNumString

      const response = await this.$axios.post(url)
      const resData = response.data
      const status = resData.applicationStage
      console.log(status)

      if (status === 'Waiting for Survey Schedule') {
        this.displayHeading = 'Waiting for schedule'
        this.displaySub =
          'The staff have not yet set a schedule for their visit to your location. Please wait for an email notification from us!'
      } else if (status === 'Pending Surveyor Visit') {
        await this.getVisit()
        this.displayHeading =
          'Your visit is scheduled on ' + this.visitationSchedule
        this.displaySub =
          'We???re on our way! Please make sure to take note of the visitation schedule.'
      }
    },
  },
})
</script>

<style lang="postcss" scoped>
/* Schedule details */
.schedule-details {
  margin-top: 10%;
  margin-left: 12%;
}

.schedule-icon {
  width: 100%;
}

.left {
  padding-top: 6%;
  width: 20%;
  float: left;
}

.right {
  width: 70%;
  margin-left: 25%;
  margin-right: 5%;
  padding-top: 13%;
}

.schedule-header {
  font-size: 180%;
}

.schedule-sub {
  margin-top: 2%;
  font-size: 100%;
}

.gray-btn-center {
  margin-top: 5%;
  text-align: center;
  padding-top: 5%;
  padding-bottom: 8%;
}

.gray-btn {
  background: #646464;
  color: #ffffff;
  box-shadow: 0px 4px 10px 6px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  padding: 1% 5% 1% 5%;
  font-size: 140%;
}

/* Welcome */
.container {
  position: relative;
  overflow: auto;
}

.welcome {
  position: absolute;
  font-family: 'Inter';
  margin-top: 8%;
  margin-left: 23%;
  font-style: normal;
  font-weight: 700;
  font-size: 250%;
  color: #000080;
}

/* Stepper */
.stepper {
  width: 44%;
  margin-top: 15%;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

/* Panel */
.panel {
  font-family: 'Inter';
  font-style: normal;
  margin-left: 12%;
  margin-right: 12%;
  margin-top: 5%;
  margin-bottom: 5%;
  background: rgba(240, 240, 240, 0.8);
  box-shadow: 0px 4px 20px 10px rgba(0, 0, 0, 0.25);
  border-radius: 20px;
}

.heading {
  font-weight: 600;
  font-size: 160%;
  padding-top: 5%;
  padding-left: 5%;
}

/* Center button */
.btn {
  background: #000080;
  color: #ffffff;
  box-shadow: 0px 4px 10px 6px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  padding: 1% 5% 1% 5%;
  font-size: 140%;
}

.center-btn {
  text-align: center;
  padding-top: 5%;
  padding-bottom: 8%;
}
</style>