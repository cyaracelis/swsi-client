<template>
  <div class="container">
    <div class="welcome">
      <p><strong>Your application number is 2211061.</strong></p>
    </div>

    <!-- Stepper temp -->
    <!-- Stepper temp -->
    <img src="~/assets/img/stepper_purchase_mats.png" class="stepper" />

    <!-- Purchase of Materials -->
    <div class="panel">
      <div class="heading">Purchase of Materials</div>

      <!-- Materials -->
      <div class="materials">
        <ol class="list-of-materials">
          <material-item v-for="m in materials" :key="m.name" :name="m.name" />
        </ol>
      </div>

      <!-- Go to Next Step -->
      <div class="center-btn">
        <button class="btn" @click="nextStep()">Go to Next Step</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  data() {
    return {
      materials: [{ name: 'Material1' }, { name: 'Material2' }],
    }
  },
  methods: {
    nextStep() {
      this.$emit('onsite-signing')
    },
  },
})
</script>

<style lang="postcss" scoped>
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

.materials {
  width: 70%;
  margin-left: auto;
  margin-right: auto;
}

.list-of-materials {
  padding-top: 2%;
  column-count: 2;
}
</style>