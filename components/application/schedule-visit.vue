<template>
  <!-- New application text -->
  <div class="container">
    <div class="welcome">
      <p><strong>Your application number is 2211061.</strong></p>
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
          <div class="schedule-header"><b>Waiting for schedule</b></div>
          <div class="schedule-sub">
            The staff have not yet set a schedule for their visit to your
            location. Please wait for an email notification from us!
          </div>
        </div>
      </div>

      <div class="gray-btn-center">
        <button class="gray-btn" @click="nextStep()">
          Please wait for further instructions. <br />Thank you!
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  methods: {
    nextStep() {
      this.$emit('purchase-materials')
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
  margin-left: 20%;
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