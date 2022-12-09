<template>
  <div class="container">
    <div class="welcome">
      <p>
        <strong>Your application number is {{ appNum }}.</strong>
      </p>
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
                ref="userId"
                v-model="file"
                class="form-input"
                chips
                :rules="fileRules"
                label="Upload .jpg, .png, or .pdf of your ID"
                required
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
            <input id="rep" v-model="rep" type="checkbox" name="rep" required />
            <label for="rep">Yes, I will be needing a representative.</label>
          </div>
        </ol>
      </div>

      <!-- Go to Next Step -->
      <div class="center-btn">
        <button class="btn" @click="upload">Go to Next Step</button>
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
      rep: false,
      file: null,
      fileRules: [
        (v) => !!v || 'File is required',
        (v) => (v && v.size > 0) || 'File is required',
        (v) => (v && v.size < 5242880) || 'File must be below 5MB.',
      ],
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

    async upload() {
      if (this.file) {
        // const options = {
        //   headers: { 'Content-Type': 'multipart/form-data' },
        // }

        const fd = new FormData()
        fd.append('validId', this.file)
        console.log(this.file)
        console.log(this.file.name)
        fd.append('hasRepresentative', 'true')

        const appNumUnknown = this.appNum as unknown
        const appNumString = appNumUnknown as string

        const url =
          'https://3498-180-190-48-16.ap.ngrok.io/applications/step2/' +
          appNumString

        console.log(url)

        try {
          await this.$axios.patch(url, fd)
        } catch (_err) {
          console.log('Error.')
          console.log(this.file)
          console.log(_err)
        }
        this.handleRequirements()
      } else {
        console.log('No file.')
      }
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
  margin-left: 23%;
  font-style: normal;
  font-weight: 700;
  font-size: 250%;
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

.form-input >>> .error--text {
  color: rgba(255, 0, 0, 1) !important;
}
</style>