<template>
  <div class="glass-panel">
    <div class="buttons">
      <div class="apply">
        <p class="btn-text">New customer?</p>
        <button class="apply-btn" @click="openApplication">Apply here</button>
        <p class="under-btn-text">More features coming soon. Stay tuned!</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  methods: {
    openApplication() {
      this.$router.push('/application')
    },
  },

  // Comment dump
  //   <div class="login">
  //         <p class="btn-text">Have any issues?</p>
  //         <button class="complaint-btn">Send a complaint</button>
  //       </div>
  //     </div>
  //     <p class="fully-experience">For any other concerns, kindly contact us.</p>
})
</script>

<style lang="postcss" scoped>
/* Panel content */
.glass-panel {
  font-family: 'Inter';
  float: right;
  margin-right: 8%;
  margin-top: 12%;
  height: 120%;
  width: 30%;
  background: #f0f0f0cc;
  opacity: 0.8;
  box-shadow: 0px 4px 20px 10px rgba(0, 0, 0, 0.25);
  /* filter: blur(2px); */
  /* backdrop-filter: blur(2px); */
  border-radius: 4%;
  text-align: center;
}

button {
  color: #ffffff;
  height: 100%;
  width: 65%;
  padding: 2% 0 2% 0;
  background: #000080;
  border-radius: 10px;
  box-shadow: 0px 4px 10px 6px rgba(0, 0, 0, 0.25);
  font-size: 130%;
  font-weight: bold;
}

.apply {
  margin-top: 15%;
  margin-bottom: 10%;
}

.login {
  margin-top: 8%;
}

.under-btn-text {
  margin-top: 3%;
}

.fully-experience {
  margin-top: 6%;
  font-size: 70%;
  margin-left: 22%;
  margin-right: 22%;
  padding-bottom: 12%;
}
</style>