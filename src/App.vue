<template>
  <v-app style="background-color: #f2f6f7">
    <v-app-bar app elevation="1" height="55" v-if="isTask">
      <div class="d-flex align-center">
      <v-btn elevation="0" @click="goToHome()">

        <v-img
          alt="Instagram logo"
          class="shrink mr-2"
          contain
          src="../src/assets/insta_name.png"
          transition="scale-transition"
          width="150"
        /></v-btn>
      </div>
      <v-spacer></v-spacer>
      <v-col col="1" sm="4" lg="3" xl="2">
        <v-text-field
          dense
          style="height: 0px"
          append-icon="mdi-magnify"
          placeholder="Search"
          class="mb-10 caption" 
          outlined
          flat

        ></v-text-field>
      </v-col>
      <v-spacer></v-spacer>

      <v-icon color="black" size="26" class="mx-2" @click="goToHome()">mdi-home</v-icon>

      <v-icon color="black" size="26" class="mx-2 mr-4">mdi-plus</v-icon>


      <v-menu
      v-model="showMenu"
      absolute
      class="mt-8"
      offset-x
      style="max-width: 600px"
    >
      <template v-slot:activator="{ on, attrs }">
        

         <v-avatar size="24" v-bind="attrs"
          v-on="on"
        ><img  src="../src/assets/background.jpg" alt="profile_pic"
      /></v-avatar>

      </template>

      <v-list>
        <v-list-item
          v-for="(item, index) in items"
          :key="index"
          router :to="item.route"
        >
          <v-list-item-title class="mr-4"><v-icon color="black" size="20" class="mr-4">{{item.icon}}</v-icon> {{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>

     



    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    showMenu: false,
    items: [
      { title: 'Profile', icon: 'mdi-account-circle-outline', route: "/profile" },
      { title: 'Saved', icon: 'mdi-bookmark-outline', route: "/saved"  },
      { title: 'Settings', icon: 'mdi-cog-outline', route: "/settings"  },
      { title: 'Logout' , icon: 'mdi-logout', route: "/logout" },
    ],
  }),

  computed:{
     isTask() {
      return (
        this.$route.name !== "Login" &&
        this.$route.name !== "SignUp" 
      );
    },
  },
   methods:{
   goToHome(){
   this.$router.push('/'); 
      }
  }
};
</script>
