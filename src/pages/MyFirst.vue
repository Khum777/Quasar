<template>
  <q-layout view="hHh Lpr lFf">
    <q-page-container class="bg-grey-2">
      <div @keyup="nextItem">
        <q-page
          padding
          class="row items-center justify-center"
          style="background: linear-gradient(#74c588, #0ad13c)"
        >
          <div class="row full-width">
            <div class="col-md-8 offset-md-2 col-xs-12 q-pa-xs">
              <q-card flat class="bg-white text-black">
                <q-card-section class="bg-blue-14">
                  <h4 class="text-h5 text-white q-my-xs text-center">
                    {{ title }}
                  </h4>
                </q-card-section>
                <div class="row full-width">
                  <div class="col-md-12 col-xs-12 q-pa-xs">
                    <q-form autofocus @submit="insertdata">
                      <q-card-section>
                        <div class="text-h6">Create New Account</div>
                        <div class="text-subtitle1">
                          Fill out the following form to create your new
                          account.
                        </div>
                      </q-card-section>
                      <q-separator inset />
                      <q-card-section class="column q-gutter-md">
                        <q-input
                          label="Name *"
                          v-model="formState.name"
                          :rules="[
                            (val) =>
                              (val && val.length > 0) ||
                              'Name must be filled in.',
                          ]"
                        ></q-input>
                        <q-input
                          label="Email *"
                          v-model="formState.email"
                          :rules="[
                            (email) =>
                              validateEmail(email) || 'Must be a valid email.',
                          ]"
                        ></q-input>
                        <q-input
                          label="Phone"
                          v-model="formState.phone"
                          mask="(###) ### - ####"
                          hint="(###) ### - ####"
                        ></q-input>
                        <q-input
                          label="Password"
                          type="password"
                          v-model="formState.password.value">

                        </q-input>
                        <q-input
                          label="Confirm Password *"
                          type="password"
                          v-model="formState.password.confirm"

                        >
                        </q-input>
                      </q-card-section>
                      <q-card-actions align="right">
                        <q-btn flat>Cancel</q-btn>
                        <q-btn color="primary" type="submit"
                        onClick="insertdata"
                          >Create Account</q-btn
                        >
                      </q-card-actions>
                    </q-form>
                  </div>
                </div>
              </q-card>
            </div>
          </div>
        </q-page>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
import axios from "axios"
export default {

  name: "MyFirst",
  components: {},
  data() {
    return {
      api:'http://localhost/myaccount2/api-account2.php',
      formState: {
        name: "",
        email: "",
        phone: "",

        password: {
          value: "",
          confirm: "",
        },
      },
    };
  },
  methods: {
    validateEmail(email) {
      return /[a-z0-9]+@[a-z]+\.[a-z]{2,3}\.[a-z]{2,3}/.test(email);
    },
    validatePassword(password) {
      var length = password.length >= 7;
      var capital = /^(?=.*[A-Z]).*$/.test(password);
      var number = /^(?=.*[0-9]).*$/.test(password);
      var symbol = /^(?=.*[!@#$%^&*-_+=]).*$/.test(password);
      return;
      length && capital && number && symbol;
    },

    insertdata(){
      axios.post(this.api,{
        action:"insert",
        name:this.formState.name,
        email:this.formState.email,
        phone:this.formState.phone,
        password:this.formState.password.value,

      }).then(res => {
        console.log(res.data);
      })
    }
  },
  mounted() {},
};
</script>

<style></style>
