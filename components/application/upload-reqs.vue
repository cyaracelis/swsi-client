<template>
  <div class="container">
    <div class="welcome">
      <p>Welcome, New Subscriber!</p>
    </div>

    <!-- Stepper temp -->
    <img src="~/assets/img/stepper_upload_reqs.png" class="stepper" />

    <!-- Uploading of Valid ID -->
    <div class="panel">
      <div class="heading">Uploading of Valid ID</div>
      <div class="steps">
        <ol class="steps-ul">
          <li>
            Kindly upload a CLEAR, SCANNED soft copy of your
            <b>VALID ID with SIGNATURE</b>. Please note that your application
            may be pended if the uploaded file does not meet these requirements.
          </li>
          <!-- Upload ID -->
          <div class="upload-id">
            <form @submit.prevent>
              <v-file-input
                model="this.userId"
                chips
                label="Upload .jpg, .png, or .pdf of your ID"
              ></v-file-input>
            </form>
          </div>
          <br />
          <li>
            Please tick the following checkbox if you require a
            <b>representative</b> to apply on your behalf during the onsite
            signing of contract and submission of requirements.
          </li>
          <div class="checkbox">
            <input id="rep" v-model="rep" type="checkbox" name="rep" />
            <label for="rep">Yes, I will be needing a representative.</label>
          </div>
        </ol>
      </div>

      <!-- Go to Next Step -->
      <div class="center-btn">
        <button class="btn" @click="handleRequirements">Go to Next Step</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  data() {
    return {
      rep: false,
    }
  },
  methods: {
    handleRequirements() {
      if (this.rep === true) {
        this.$emit('rep-info')
      } else {
        this.$emit('print-forms')
      }
    },

    async upload(ev: Event) {
      const files = (ev.target as HTMLInputElement).files
      if (!files) {
        return
      }

      const file = files[0]
      const fd = new FormData()
      fd.append('file', file, file.name)

      try {
        await this.$axios.post('http://localhost:3000/applications/step2', fd)
      } catch (_err) {
        console.log('POST error')
      }
      this.handleRequirements()
    },
  },
})
</script>

<style lang="postcss" scoped>
/* Steps */
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
  align: center;
  color: #000080;
}

/* Stepper */
.stepper {
  width: 44%;
  margin-top: 13%;
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
  margin-top: 3%;
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

/* Input fields */
.row {
  padding-top: 2%;
  padding-left: 5%;
}

.steps {
  padding-top: 2%;
  padding-left: 7%;
  padding-right: 15%;
}

.steps-ul {
  font-weight: 400;
}

li {
  padding-bottom: 2%;
}

/* Upload ID */
.filename {
  background: #ffffff;
  float: left;
  padding: 1% 5% 1% 5%;
}

.upload-btn-icon {
  width: 20%;
  float: left;
}

.upload-field {
  padding-bottom: 2%;
}

/* Representative  checkbox */
.checkbox {
  padding-left: 2%;
}
</style>