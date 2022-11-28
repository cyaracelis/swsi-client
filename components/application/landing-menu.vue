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
        id="application-num"
        type="text"
        name="application-num"
        class="application-num"
        placeholder="Application Number"
      />
      <button class="continue-btn">Continue</button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  methods: {
    newApplication() {
      this.$emit('customer-info')
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