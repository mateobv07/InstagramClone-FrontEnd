<template>
  <v-container>
    <v-row justify="center" no-gutters>
      <v-col :md="$vuetify.breakpoint.lg ? 8 : $vuetify.breakpoint.md ? 10 : $vuetify.breakpoint.smAndDown ? 12 : 5" offset-xl="0" >
        <hello-world class="pt-8" />
        <post v-for="i in posts" :key="`${i}`" :username="i.username" :profile_picture="i.profile_picture" :post_picture="i.post_picture"  :post_likes="i.post_likes" :post_description="i.post_description" :post_comments="i.post_comments" :post_tags="i.post_tags"/>
      </v-col>
      <v-col v-if="!$vuetify.breakpoint.smAndDown" class="pt-12" md="2">
        <div style="position: sticky; top: 105px">
        <v-row class="ml-n16">
          <v-avatar size="60">
            <img src="../assets/background.jpg" alt="profile_pic" />
          </v-avatar>
          <v-col>
            <h4 class="text-subtitle-2 pl-2 ">Username</h4>
            <h4 class="text-subtitle-2 pl-2 mt-n1" style="opacity:50%;">Real name</h4>
          </v-col>
          <button text class="blue--text"> <p class="text-subtitle-2">Logout</p></button>
        </v-row>
        
        <v-row>
          <h4 class="text-subtitle-2 ml-n14 mt-5" style="opacity:60%;">Suggestions for your </h4>
        </v-row>

        <v-row v-for="i in 5" :key="`${i}`" class="ml-n16">
          <v-avatar size="36" class="mt-3">
            <img src="../assets/background.jpg" alt="profile_pic" />
          </v-avatar>
          <v-col>
            <h4 class="text-subtitle-2 pl-1 ">Username</h4>
            <h4 class="caption pl-1 mt-n1" style="opacity:70%;">Real name</h4>
          </v-col>
          <button text class="blue--text"> <p class="caption">Follow</p></button>
        </v-row>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import HelloWorld from "../components/story_bar.vue";
import Post from "../components/post.vue";

export default {
  name: "Home",

  components: {
    HelloWorld,
    Post,
  },
  data: () => ({
    dialog: false,
    posts:[
      {
        "username" : "Usuario",
        "profile_picture" : "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        "post_picture" : "https://wallpaperaccess.com/full/31193.jpg",
        "post_likes" : 200,
        "post_description" : "Usuario Insta life lol lorem ipsum",
        "post_comments" : [{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},],
        "date_created" : "",
        "post_tags" : ["mateobv07", "cristianoRonaldo"],
        },
      {
        "username" : "Usuario",
        "profile_picture" : "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        "post_picture" : "https://wallpapercave.com/wp/wp4576169.jpg",
        "post_likes" : 200,
        "post_description" : "Usuario Insta life lol lorem ipsum",
        "post_comments" : [{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},],
        "date_created" : "",
        "post_tags" : ["mateobv07", "cristianoRonaldo"],
      },
      {
        "username" : "Usuario",
        "profile_picture" : "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        "post_picture" : "https://us.123rf.com/450wm/kostsov/kostsov1906/kostsov190600026/126080344-modern-showcase-with-empty-space-on-pedestal-on-blue-background-3d-rendering-.jpg?ver=6",
        "post_likes" : 200,
        "post_description" : "Usuario Insta life lol lorem ipsum",
        "post_comments" : [{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},],
        "date_created" : "",
        "post_tags" : [],
      },
      {
        "username" : "Usuario",
        "profile_picture" : "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        "post_picture" : "https://wallpaperaccess.com/full/1269989.jpg",
        "post_likes" : 200,
        "post_description" : "Usuario Insta life lol lorem ipsum",
        "post_comments" : [{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},],
        "date_created" : "",
        "post_tags" : ["mateobv07", "cristianoRonaldo"],
      },
      {
        "username" : "Usuario",
        "profile_picture" : "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        "post_picture" : "https://us.123rf.com/450wm/kostsov/kostsov1906/kostsov190600026/126080344-modern-showcase-with-empty-space-on-pedestal-on-blue-background-3d-rendering-.jpg?ver=6",
        "post_likes" : 200,
        "post_description" : "Usuario Insta life lol lorem ipsum",
        "post_comments" : [{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},],
        "date_created" : "",
        "post_tags" : [],
      },
      {
        "username" : "Usuario",
        "profile_picture" : "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        "post_picture" : "https://wallpaperaccess.com/full/31193.jpg",
        "post_likes" : 200,
        "post_description" : "Usuario Insta life lol lorem ipsum",
        "post_comments" : [{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},],
        "date_created" : "",
        "post_tags" : [],
      },
      {
        "username" : "Usuario",
        "profile_picture" : "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        "post_picture" : "https://us.123rf.com/450wm/kostsov/kostsov1906/kostsov190600026/126080344-modern-showcase-with-empty-space-on-pedestal-on-blue-background-3d-rendering-.jpg?ver=6",
        "post_likes" : 200,
        "post_description" : "Usuario Insta life lol lorem ipsum",
        "post_comments" : [{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},],
        "date_created" : "",
        "post_tags" : [],
      },
      {
        "username" : "Usuario",
        "profile_picture" : "https://images.pexels.com/photos/1034662/pexels-photo-1034662.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
        "post_picture" : "https://images.pexels.com/photos/1034662/pexels-photo-1034662.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
        "post_likes" : 200,
        "post_description" : "Usuario Insta life lol lorem ipsum",
        "post_comments" : [{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},],
        "date_created" : "",
        "post_tags" : [],
      },
      {
        "username" : "Usuario",
        "profile_picture" : "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        "post_picture" : "https://cdn.pixabay.com/photo/2016/05/05/02/37/sunset-1373171__480.jpg",
        "post_likes" : 200,
        "post_description" : "Usuario Insta life lol lorem ipsum",
        "post_comments" : [{"username":"Elver", "comment": "So cool, where was this taken?" },{"username":"Mateobv07", "comment": "Lorem impsum xasxs csdc wewsa leasd cexer"},],
        "date_created" : "",
        "post_tags" : [],
      },
    ],
  }),
};
</script>
