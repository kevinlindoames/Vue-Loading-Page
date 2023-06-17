<template>
  <v-app>
    <div class="backgruond"></div>
    <v-main class="d-flex justify-center align-center">
      <v-col cols="10" lg="4" class="mx-auto">
        <v-card class="pa-4">
          <div class="text-center">
            <v-avatar size="100" color="indigo lighten-4">
              <v-icon size="40" color="indigo">mdi-account</v-icon>
            </v-avatar>
            <h2 class="indigo--text">Vue Login Page</h2>
          </div>
          <v-form @submit.prevent="submithandler" ref="form">
            <v-card-text>
              <v-text-field
                v-model="email"
                :rules="emailRules"
                label="Email"
                outlined
                prepend-inner-icon="mdi-email"
                type="email"
              />
              <v-text-field
                v-model="password"
                :rules="passwordRules"
                :type="passwordShow ? 'text' : 'password'"
                label="Password"
                outlined
                prepend-inner-icon="mdi-lock"
                :append-icon="passwordShow ? 'mdi-eye' : 'mdi-eye-off'"
                @click:append="passwordShow = !passwordShow" required
                
              />
              <v-switch
                label="Remember Me"
                color="indigo"
                class="mt-4"
              ></v-switch>
            </v-card-text>
            <v-card-actions class="justify-center">
              <v-btn :loading="loading" type="submit" color="indigo">
                <span class="white--text px-8">Login</span>
              </v-btn>
            </v-card-actions>
          </v-form>
        </v-card>
      </v-col>
    </v-main>
    <v-snackbar color="success"
      v-model="snackbar"      
      > Login Succes
      </v-snackbar>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    loading: false,
    snackbar: false,
    passwordShow: false,
    password: "",
    passwordRules: [
      (v) => !!v || "Password is required",
      (v) => (v && v.length >= 8) || "Min 8 characters",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
    //
  }),
  methods: {
    submithandler() {
      if (this.$refs.form.validate()) {
        this.loading = true
        setTimeout(() => {
          this.loading = false
          this.snackbar = true
        }, 3000);
      }
    }
  }
};
</script>

<style>
.backgruond {
  background-image: url(./assets/Order-Banner.jpg) !important;
  width: 100%;
  height: 300px;
  display: block;
  position: absolute;
  top: 0;
  background-size: cover;
}
</style>
