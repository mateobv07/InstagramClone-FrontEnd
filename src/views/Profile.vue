<template>
  <div class="profile">
    <v-container>
      <v-row no-gutters justify="center" class="mt-5">
        <v-col lg="2" md="4">
          <v-avatar size="150">
            <img src="../assets/background.jpg" alt="profile_pic" />
          </v-avatar>
        </v-col>
        <v-col xl="4" md="8">
          <v-row class="mt-5">
            <h4 class="text-h5">{{username}}</h4>
            <v-btn elevation="0" class="light-blue darken-1 ml-5" height="30"> <p class="white--text pt-4"> Follow </p></v-btn>
            <v-icon class="ml-4" color="black">mdi-dots-horizontal</v-icon>
          </v-row>
          <v-row class="mt-5">
            <p class="pt-3"> <b>{{posts}}  </b>posts </p>
            <p class="pt-3 ml-6"> <b>{{followers}}  </b>followers </p>
            <p class="pt-3 ml-6"> <b>{{following}}  </b>following </p>
          </v-row>
          <v-row class="mt-5">
            <p class="font-weight-medium">{{user_real_name}}   </p>
          </v-row>
          <v-row class="mt-0 mb-5">
            <p >{{user_description}}   </p>
          </v-row>
        </v-col>
      </v-row>

      <v-divider></v-divider>
      <v-row
        class="mt-6"
        align="center"
        justify="center"
        v-for="n in 4"
        :key="n"
      >
      
        <v-col :md="$vuetify.breakpoint.mdAndDown ? 4 : 0" :class="$vuetify.breakpoint.lgAndUp ? 'shrink': '' " align="center" v-for="n in 3" :key="n">
            <v-img
              alt="post"
              lazy-src="../assets/post_img.jpg"
              height="290"
              width="290"
              src="../assets/post_img.jpg"
            ></v-img>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "Profile",

  components: {
    //
  },
  data: () => ({
    posts: 5,
    followers: 243,
    following: 324,
    user_real_name: "Real name",
    username: "User",
    user_description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin convallis iaculis urna, id lobortis tortor vulputate at. Sed luctus, massa sed euismod gravida, ex"
  }),
};
</script>
