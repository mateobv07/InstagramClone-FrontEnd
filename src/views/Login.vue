<template>
  <div class="login">
    <v-container >
      <v-row justify="center" align="center">
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
          height="500"
          width="350"
        ></v-sheet>
        <v-sheet
          class="ma-5"
          color="white"
          elevation="1"
          height="100"
          width="350"
        ></v-sheet>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
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
    username: "User",
    user_description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin convallis iaculis urna, id lobortis tortor vulputate at. Sed luctus, massa sed euismod gravida, ex",
  }),
};
</script>
