<template>
  <div class="container">
    <!-- New application text -->
    <div class="welcome">
      <p>Welcome, New Subscriber!</p>
    </div>

    <!-- Stepper temp -->
    <img src="~/assets/img/stepper_customer_info.png" class="stepper" />

    <!-- Application form -->
    <div class="panel">
      <div class="heading">New Customer Application</div>

      <v-form
        id="app-form"
        ref="form"
        v-model="valid"
        lazy-validation
        class="application-form"
        @submit.prevent="onSubmit()"
      >
        <v-container>
          <v-row></v-row>
          <v-row> <h3 class="h3">Customer Information</h3></v-row>
          <v-row> <h3></h3></v-row>

          <!-- FIRST ROW -- Names -->
          <v-layout>
            <v-spacer />
            <v-flex xs12 md3>
              <v-text-field
                v-model="user.firstName"
                :rules="nameRules"
                class="form-input"
                :counter="15"
                label="First name"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />

            <v-flex xs12 md3>
              <v-text-field
                v-model="user.middleName"
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
                v-model="user.lastName"
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
                v-model="user.email"
                class="form-input ml-5"
                :rules="emailRules"
                label="Email"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />

            <v-flex xs12 md7>
              <v-text-field
                v-model="user.establishmentName"
                class="form-input text-mr"
                :rules="optionalRules"
                label="(Optional) If commercial, Official Name of Establishment"
              ></v-text-field>
            </v-flex>
            <v-spacer />
          </v-layout>

          <!--THIRD ROW -- CONTACT 2 -->
          <v-layout>
            <v-spacer />
            <v-flex xs1 md3>
              <v-text-field
                v-model="user.contactNo"
                class="form-input ml-5"
                :rules="numberRules"
                label="Contact number"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />

            <v-flex xs1 md7>
              <v-text-field
                v-model="user.address"
                class="form-input mr-5"
                :rules="nameRules"
                label="Address"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />
          </v-layout>

          <!--FOURTH ROW -- CONTACT 3 -->
          <v-layout>
            <v-spacer />
            <v-flex xs5 md10>
              <v-text-field
                v-model="user.landmark"
                class="form-input ml-5"
                :rules="optionalRules"
                label="Landmarks and/or remarks"
              ></v-text-field>
            </v-flex>
            <v-spacer />
            <v-spacer />
          </v-layout>
        </v-container>

        <v-container>
          <v-row> <h3 class="h3">Reference Account</h3></v-row>
          <v-row> <h3></h3></v-row>

          <!-- FIRST ROW -- Names -->
          <v-layout>
            <v-spacer />
            <v-flex xs12 md3>
              <v-text-field
                v-model="user.refFirstName"
                :rules="nameRules"
                class="form-input"
                :counter="15"
                label="First name"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />

            <v-flex xs12 md3>
              <v-text-field
                v-model="user.refMiddleName"
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
                v-model="user.refLastName"
                class="form-input"
                :counter="15"
                :rules="nameRules"
                label="Last name"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />
          </v-layout>

          <!--SECOND ROW -- ETC  -->
          <v-layout>
            <v-spacer />
            <v-flex xs12 md3>
              <v-text-field
                v-model="user.refClientNo"
                class="form-input ml-5"
                :rules="numberRules"
                label="Account Number"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />

            <v-flex xs12 md7>
              <v-text-field
                v-model="user.refAddress"
                class="form-input mr-5"
                :rules="nameRules"
                label="Reference Address"
                required
              ></v-text-field>
            </v-flex>
            <v-spacer />
          </v-layout>
        </v-container>
        <div class="center-btn">
          <button class="btn" input type="submit" value="Submit">
            Submit Application
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
      user: {
        firstName: '',
        middleName: '',
        lastName: '',
        email: '',
        contactNo: '',
        establishmentName: '',
        address: '',
        landmark: '',
        refFirstName: '',
        refMiddleName: '',
        refLastName: '',
        refClientNo: '',
        refAddress: '',
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
      appNum: 0,
    }
  },

  methods: {
    nextPage() {
      this.$emit('upload-reqs')
    },

    async onSubmit() {
      try {
        const options = {
          headers: { 'content-type': 'application/json' },
        }

        const res = await this.$axios.post(
          'https://3498-180-190-48-16.ap.ngrok.io/applications/step1',
          {
            firstName: this.user.firstName,
            middleName: this.user.middleName,
            lastName: this.user.lastName,
            email: this.user.email,
            contactNo: this.user.contactNo,
            establishmentName: this.user.establishmentName,
            address: this.user.address,
            refClientNo: this.user.refClientNo,
            refFirstName: this.user.refFirstName,
            refMiddleName: this.user.refMiddleName,
            refLastName: this.user.refLastName,
            landmark: this.user.landmark,
            ownership: 'leased',
            connectionType: 'Tapping',
          },
          options
        )

        const responseData = res.data
        const appNum: Number = responseData.applicationNo
        console.log(appNum)
        this.$set(this, 'appNum', appNum)
        this.$emit('set-app-num', appNum)
        this.nextPage()
      } catch (err: any) {
        console.log(err)
      }
    },
  },
})
</script>

<style lang="postcss" scoped>
.container {
  position: relative;
  overflow: auto;
}
/* Welcome */
.welcome {
  position: absolute;
  font-family: 'Inter';
  margin-top: 4%;
  margin-left: 27%;
  font-style: normal;
  font-weight: 700;
  font-size: 250%;
  text-align: center;
  color: #000080;
}

/* Stepper */
.stepper {
  width: 44%;
  margin-top: 10%;
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

.subheading {
  font-weight: 300;
  font-size: 120%;
  padding-top: 5%;
}

.h3 {
  font-weight: 400;
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

.field {
  display: flex;
  flex-direction: column;
  padding-right: 2%;
}

.form-input >>> .error--text {
  color: rgba(255, 0, 0, 1) !important;
}
</style>