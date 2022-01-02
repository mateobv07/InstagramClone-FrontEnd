<template>
  <div class="login">
    <v-container >
      <v-row justify="center" align="center" class="mt-12">
      <v-col align="center" class="shrink" >
        <v-img
          lazy-src="../assets/insta_login.png"
          max-width="370"
          src="../assets/insta_login.png"
        ></v-img>
      </v-col>
        <v-col align="center" class="shrink" >
        <v-sheet
          class="ma-5"
          color="white"
          elevation="1"
          height="380"
          width="350"
        >
        <v-col >
        <v-img
        class="my-4"
          lazy-src="../assets/insta_name.png"
          max-width="180"
          src="../assets/insta_name.png"
        ></v-img>
        <v-text-field
        v-model="username"
            filled        
            class="mx-7 pt-4 rounded-1"
            label="Email or Username"
            outlined
            dense
          ></v-text-field>
          <v-text-field
          v-model="password"
            :append-icon="show3 ? 'mdi-eye' : 'mdi-eye-off'"
            :type="show3 ? 'text' : 'password'"
            filled        
            class="mx-7 mt-n5 rounded-1"
            label="Password"
            outlined
            dense
            @click:append="show3 = !show3"
          ></v-text-field>
          <v-btn @click="login()" color="light-blue darken-1" width="270" height="32" class="mt-n3">
          <p class="white--text text-button mt-5">Login</p>
          </v-btn>
          <v-divider class="mt-7 mx-7"></v-divider>
          <p class="text-body-2 pt-9"> <a>Forgot Password?</a></p>
          </v-col>
        </v-sheet>
        <v-sheet
          class="ma-5 mt-n2"
          color="white"
          elevation="1"
          height="65"
          width="350"
        >
        <p class="text-body-2 pt-6">Dont have an account? <a href="/signup"><b>Sign Up</b></a></p>
        </v-sheet>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import axios from "axios"
export default {
  name: "Login",

  components: {
    //
  },
  data: () => ({
    posts: 5,
    followers: 243,
    following: 324,
    user_real_name: "Real name",
    username: "",
    password: "",
    show3: false,
    auth_token:"",
    user_description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin convallis iaculis urna, id lobortis tortor vulputate at. Sed luctus, massa sed euismod gravida, ex",
  }),
  methods: {
    login() {
      var vueinstance = this;
      axios({
        method: "post",
        url: "http://127.0.0.1:8000/account/login/",
        data: {
          username: this.username,
          password: this.password,
        },
      })
        .then(function (response) {
          console.log(response.data)
          vueinstance.auth_token = response.data.token
          vueinstance.$router.push('/') 
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  }
};
</script>
