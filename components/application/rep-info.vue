<template>
  <div class="container">
    <!-- New application text -->
    <div class="welcome">
      <p>Your application number is {{ appNum }}.</p>
    </div>

    <!-- Stepper temp -->
    <img src="~/assets/img/stepper_upload_reqs.png" class="stepper" />

    <!-- Representative Requirements and Information -->
    <div class="panel">
      <div class="heading">Representative Requirements and Information</div>
      <v-form
        id="app-form"
        ref="form"
        v-model="valid"
        lazy-validation
        class="application-form"
        @submit.prevent="onSubmit()"
      >
        <v-container>
          <v-row> <h3 class="h3">Customer Information</h3></v-row>
          <v-row> <h3></h3></v-row>

          <!-- FIRST ROW -- Names -->
          <v-layout>
            <v-spacer />
            <v-flex xs12 md3>
              <v-text-field
                v-model="rep.firstName"
                class="form-input"
                :rules="nameRules"
                :counter="15"
                label="First name"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />

            <v-flex xs12 md3>
              <v-text-field
                v-model="rep.middleName"
                class="form-input mx-2"
                :rules="nameRules"
                :counter="15"
                label="Middle name"
                required
              ></v-text-field>
            </v-flex>

            <v-spacer />
            <v-flex xs12 md3>
              <v-text-field
                v-model="rep.lastName"
                class="form-input"
                :counter="15"
                :rules="nameRules"
                label="Last name"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />
          </v-layout>

          <!--SECOND ROW -- CONTACT -->
          <v-layout>
            <v-spacer />
            <v-flex xs12 md3>
              <v-text-field
                v-model="rep.email"
                class="form-input ml-5"
                label="Email"
              ></v-text-field>
            </v-flex>
            <v-spacer />

            <v-flex xs1 md3>
              <v-text-field
                v-model="rep.contactNo"
                class="form-input ml-5"
                :rules="numberRules"
                label="Contact number"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />

            <v-flex xs12 md3>
              <v-text-field
                v-model="rep.relationship"
                class="form-input"
                :counter="15"
                :rules="nameRules"
                label="Relationship"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />
          </v-layout>
        </v-container>

        <!-- Upload ID -->
        <div class="upload-id">
          <v-flex xs12 md11>
            <form @submit.prevent>
              <v-file-input
                v-model="file"
                class="form-input"
                model="this.userId"
                :rules="fileRules"
                chips
                required
                label="Upload .jpg, .png, or .pdf of representative's ID with signature (max 5MB)."
              ></v-file-input>
            </form>
          </v-flex>
        </div>

        <div class="center-btn">
          <button
            class="btn"
            input
            type="submit"
            value="Submit"
            @click="onSubmit"
          >
            Submit Representative Info
          </button>
        </div>
      </v-form>
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
      rep: {
        firstName: '',
        middleName: '',
        lastName: '',
        email: '',
        contactNo: '',
        relationship: '',
      },
      valid: false,
      nameRules: [(v) => !!v || 'This field is required'],
      optionalRules: [],
      numberRules: [
        (v) => !!v || 'This field is required',
        (v) => Number.isInteger(Number(v)) || 'Please input a number',
      ],
      file: null,
      fileRules: [
        (v) => !!v || 'File is required',
        (v) => (v && v.size > 0) || 'File is required',
        (v) => (v && v.size < 5242880) || 'File must be below 5MB.',
      ],
    }
  },
  methods: {
    nextStep() {
      this.$emit('print-forms')
    },

    async onSubmit() {
      const appNumUnknown = this.appNum as unknown
      const appNumString = appNumUnknown as string

      const url =
        'https://3498-180-190-48-16.ap.ngrok.io/applications/step2a/' +
        appNumString

      console.log(url)

      if (this.file) {
        const fd = new FormData()
        fd.append('validId', this.file)
        console.log(this.file)

        fd.append('firstName', this.rep.firstName)
        fd.append('middleName', this.rep.middleName)
        fd.append('lastName', this.rep.lastName)
        fd.append('contactNo', this.rep.contactNo)
        fd.append('relationship', this.rep.relationship)
        if (this.rep.email) {
          fd.append('email', this.rep.email)
        }

        try {
          await this.$axios.post(url, fd)
          this.nextStep()
        } catch (_err) {
          console.log('Error.')
          console.log(this.file)
          console.log(_err)
        }
      }
    },
  },
})
</script>

<style lang="postcss" scoped>
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

.upload-id {
  padding-top: 2%;
  padding-left: 5%;
}

/* Input fields */
.row {
  padding-top: 2%;
  padding-left: 5%;
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

.h3 {
  font-weight: 400;
}

.center-btn {
  text-align: center;
  padding-top: 5%;
  padding-bottom: 8%;
}

.form-input >>> .error--text {
  color: rgba(255, 0, 0, 1) !important;
}
</style>