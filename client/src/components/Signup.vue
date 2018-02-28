<template>
  <v-layout column>
    <v-flex md6 offset-md3>
      <div class="white elevation-2">
        <v-toolbar dark color="primary">
          <v-toolbar-title>Register</v-toolbar-title>
        </v-toolbar>
        <v-container>
          <v-form v-model="valid" @submit.prevent="register()">
            <v-text-field label="Username" v-model="username" :rules="usernameRules" required></v-text-field>
            <v-text-field label="Full Name" v-model="fullname" :rules="fullnameRules" required></v-text-field>
            <v-text-field type="password" label="Password" v-model="password" :rules="passwordRules" required></v-text-field>
            <v-btn type="submit" color="primary">Register</v-btn>
          </v-form>
        </v-container>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
  import services from '../services';

  export default {
    data() {
      return {
        valid: false,
        username: '',
        password: '',
        fullname: '',
        error: {},
        usernameRules: [
          v => !!v || 'Username is required.',
          v => v.length >= 5 || 'username must be at least 5 characters long.',
        ],
        fullnameRules: [
          v => !!v || 'Full name is required..',
          v => v.length >= 3 || 'Full name must be at least 3 characters long.',
        ],
        passwordRules: [
          v => !!v || 'Password is required..',
          v => v.length >= 3 || 'Password must be at least 3 characters long.',
        ],
      };
    },
    methods: {
      async register() {
        if (this.valid) {
          try {
            await services.register({
              username: this.username,
              fullname: this.fullname,
              password: this.password,
            });
            this.$router.push('/login');
            swal({
              title: 'Thanks for Sign Up',
              text: 'You have create your account',
              icon: 'success',
              button: 'Continue'
            })
          } catch (error) {
            throw new Error(error);
          }
        }
      },
    },
    beforeCreate() {
      if (this.$store.getters.token) {
        this.$router.push('/');
      }
    },
  };

</script>

<style scoped>


</style>
