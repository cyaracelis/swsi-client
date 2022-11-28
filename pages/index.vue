<template>
  <div class="body-cover">
    <nav-bar />

    <div class="landing-content">
      <!-- Landing text -->
      <div class="text">
        <div class="heading">A water system you can trust.</div>
        <div class="sub">
          Providing standard pressure, sanitary and potable water 24/7 in
          Mexico, Pampanga since 2005.
        </div>
      </div>

      <!-- Panel -->
      <landing-panel />
    </div>
  </div>
</template>
  
  <script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
})
</script>
  
  <style lang="postcss" scoped>
.body-cover {
  background-size: cover;
  height: 100vh;
  overflow: hidden;
  background-image: url('~/assets/img/home_bg.png');
}

/* Landing text */
.landing-content {
  z-index: 98;
}

.text {
  font-family: 'Inter';
  float: left;
  margin-left: 4%;
  width: 55%;
  opacity: 1;
}

.heading {
  font-size: 260%;
  color: #3671dc;
  margin-top: 30%;
  font-weight: bold;
}

.sub {
  width: 70%;
  text-align: justify;
  font-size: 138%;
  padding-top: 7%;
}
</style>
  