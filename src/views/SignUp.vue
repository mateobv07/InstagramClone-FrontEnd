<template>
  <div class="signup">
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
          height="520"
          width="350"
        >
        <v-col >
        <v-img
        class="my-4"
          lazy-src="../assets/insta_name.png"
          max-width="180"
          src="../assets/insta_name.png"
        ></v-img>
        <h4 class="mb-n5 mx-7" style="opacity:60%;">Sign up to see photos and videos from your friends.</h4>
        <v-divider class="mt-7 mx-7"></v-divider>
        <v-text-field
            v-model="email"
            filled        
            class="mx-7 pt-4 rounded-1"
            label="Email"
            outlined
            dense
          ></v-text-field>
          <v-text-field
          v-model="real_name"
            filled        
            class="mx-7 mt-n4 rounded-1"
            label="Full Name"
            outlined
            dense
          ></v-text-field>
           <v-text-field
            filled        
            v-model="username"
            class="mx-7 mt-n4 rounded-1"
            label="Username"
            outlined
            dense
          ></v-text-field>
           <v-text-field
           v-model="password"
            filled        
            class="mx-7 mt-n4 rounded-1"
            label="Password"
            password
              :append-icon="show3 ? 'mdi-eye' : 'mdi-eye-off'"
              :type="show3 ? 'text' : 'password'"
            outlined
            dense
            @click:append="show3 = !show3"
          ></v-text-field>
          <v-btn   @click="signup()"  color="light-blue darken-1" width="270" height="32" class="mt-n3">
          <p class="white--text text-button mt-5">Sign Up</p>
          </v-btn>
          
          <p class="text-caption pt-9 px-7" style="opacity:70%;">By signing up, you agree to our Terms , Data Policy and Cookies Policy . </p>
          </v-col>
        </v-sheet>
        <v-sheet
          class="ma-5 mt-n2"
          color="white"
          elevation="1"
          height="65"
          width="350"
        >
        <p class="text-body-2 pt-6">Already have an account? <a href="/login"><b> Login</b></a></p>
        </v-sheet>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "SignUp",

  components: {
    //
  },
  data: () => ({
    posts: 5,
    followers: 243,
    following: 324,
    real_name: "",
    username: "",
    show3: false,
    email: "",
    password: "",
    user_description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin convallis iaculis urna, id lobortis tortor vulputate at. Sed luctus, massa sed euismod gravida, ex",
  }),
  methods: {
    signup() {
      var vueinstance = this;
      axios({
        method: "post",
        url: "http://127.0.0.1:8000/account/signup/",
        data: {
          email: this.email,
          username: this.username,
          real_name: this.real_name,
          password: this.password,
        },
      })
        .then(function (response) {
          console.log(response.data)
          vueinstance.$router.push('Profile') 
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  }
};
</script>