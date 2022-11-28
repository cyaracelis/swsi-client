<template>
  <div class="container">
    <div class="welcome">
      <p>Welcome, New Subscriber!</p>
    </div>

    <!-- Stepper temp -->
    <img src="~/assets/img/stepper_print_forms.png" class="stepper" />

    <!-- Printing and Preparation of Requirements -->
    <div class="panel">
      <div class="heading">Printing and Preparation of Requirements</div>
      <table>
        <tr>
          <th>Printed Requirements (to bring onsite)</th>
          <th>Click to print:</th>
        </tr>
        <tr>
          <td>1. One (1) copy of accomplished Application Form</td>
          <td>
            <button
              class="print-btn"
              href="http://localhost:3000/applications/step3-1/0'"
              @click="download(1)"
            >
              <img
                src="~assets/img/print_forms_button.png"
                class="print-btn-icon"
              />
              <p>Print</p>
            </button>
          </td>
        </tr>
        <tr>
          <td>2. Two (2) signed copies of Customer Reminders document</td>
          <td>
            <button
              class="print-btn"
              href="http://localhost:3000/applications/step3-2/0'"
              @click="download(2)"
            >
              <img
                src="~assets/img/print_forms_button.png"
                class="print-btn-icon"
              />
              <p>Print</p>
            </button>
          </td>
        </tr>
        <tr>
          <td>
            3. One (1) signed Authorization Letter* <br />
            *Only if a representative will apply on your behalf
          </td>
          <td>
            <button
              class="print-btn"
              href="http://localhost:3000/applications/step3-3/0'"
              @click="download(3)"
            >
              <img
                src="~assets/img/print_forms_button.png"
                class="print-btn-icon"
              />
              <p>Print</p>
            </button>
          </td>
        </tr>
      </table>

      <!-- Go to Next Step -->
      <div class="center-btn">
        <button class="btn" @click="nextStep">Go to Next Step</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  methods: {
    nextStep() {
      this.$emit('schedule-visit')
    },

    download(formNum: number) {
      if (formNum === 1) {
        window.open('http://localhost:3000/applications/step3-1/0')
      } else if (formNum === 2) {
        window.open('http://localhost:3000/applications/step3-2/0')
      } else {
        window.open('http://localhost:3000/applications/step3-3/0')
      }
    },
  },
})
</script>

<style lang="postcss" scoped>
table {
  border-collapse: collapse;
}

table,
td,
th {
  padding: 1% 1% 1% 1%;
  margin-top: 5%;
  margin-left: auto;
  margin-right: auto;
  border: 1px solid;
}

/* Print button */
.print-btn-icon {
  width: 20%;
  float: left;
  vertical-align: middle;
}

.print-btn {
  text-align: center;
}

/* Font links*/
@import url('https://fonts.googleapis.com/css?family=Inter');

/* Welcome */
.container {
  position: relative;
  overflow: auto;
}

.welcome {
  position: absolute;
  font-family: 'Inter';
  margin-top: 8%;
  margin-left: 27%;
  font-style: normal;
  font-weight: 700;
  font-size: 250%;
  color: #000080;
}

/* Stepper */
.stepper {
  width: 44%;
  margin-top: 18%;
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