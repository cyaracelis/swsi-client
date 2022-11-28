<template>
  <div class="container">
    <!-- New application text -->
    <div class="welcome">
      <p>Welcome, New Subscriber!</p>
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
          <v-row><v-subheading> </v-subheading></v-row>
          <v-row> <v-title> Customer Information </v-title></v-row>
          <v-row> <v-title> </v-title></v-row>

          <!-- FIRST ROW -- Names -->
          <v-layout>
            <v-spacer />
            <v-flex xs12 md3>
              <v-text-field
                v-model="rep.firstName"
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
                class="mx-2"
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
                class="ml-5"
                :rules="emailRules"
                label="Email"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />

            <v-flex xs1 md3>
              <v-text-field
                v-model="rep.contactNo"
                class="ml-5"
                :rules="numberRules"
                label="Contact number"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />

            <v-flex xs12 md3>
              <v-text-field
                v-model="rep.relationship"
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
                model="this.userId"
                chips
                label="Upload .jpg, .png, or .pdf of representative's ID with signature"
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
            @click="nextStep"
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
      emailRules: [
        (v) => !!v || 'E-mail is required',
        (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
    }
  },
  methods: {
    nextStep() {
      this.$emit('print-forms')
    },

    async onSubmit() {},
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