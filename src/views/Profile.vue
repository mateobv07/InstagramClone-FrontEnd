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
            <h4 class="text-h5">{{ username }}</h4>
            <v-btn elevation="0" class="light-blue darken-1 ml-5" height="30">
              <p class="white--text pt-4">Follow</p></v-btn
            >
            <v-icon class="ml-4" color="black">mdi-dots-horizontal</v-icon>
          </v-row>
          <v-row class="mt-5">
            <p class="pt-3">
              <b>{{ posts.length }} </b>posts
            </p>
            <p class="pt-3 ml-6">
              <b>{{ followers }} </b>followers
            </p>
            <p class="pt-3 ml-6">
              <b>{{ following }} </b>following
            </p>
          </v-row>
          <v-row class="mt-5">
            <p class="font-weight-medium">{{ user_real_name }}</p>
          </v-row>
          <v-row class="mt-0 mb-5">
            <p>{{ user_description }}</p>
          </v-row>
        </v-col>
      </v-row>

      <v-divider></v-divider>
       <v-bottom-navigation
    :value="value"
    color="primary"
    horizontal
    width="500"
    class="mx-auto mb-n6 elevation-0"
    style="background-color: #f2f6f7"

  >
    <v-btn>
      <span class="ml-n2">POSTS</span>

      <v-icon size="18" class="mr-3">mdi-grid</v-icon>
    </v-btn>

    <v-btn class="mx-6">
      <span class="ml-n2">SAVED</span>

      <v-icon size="18" class="mr-3">mdi-bookmark-outline</v-icon>
    </v-btn>

    <v-btn>
      <span class="ml-n2">TAGGED</span>

      <v-icon size="18" class="mr-3">mdi-account-box-outline</v-icon>
    </v-btn>
  </v-bottom-navigation>
      <v-row
        class="mt-6"
        align="center"
        justify="center"
        v-for="n in Math.ceil(posts.length / 3)"
        :key="n"
      >
        <v-col
          :md="$vuetify.breakpoint.mdAndDown ? 4 : 0"
          :class="$vuetify.breakpoint.lgAndUp ? 'shrink' : ''"
          align="center"
          v-for="i in 3"
          :key="i"
        >
          <v-dialog v-model="viewPost" max-width="1400">
            <template v-slot:activator="{ on, attrs }">
              <v-hover v-slot="{ hover }">
                <v-img
                  :class="{ 'on-hover': hover }"
                  v-bind="attrs"
                  v-on="on"
                  alt="post"
                  :lazy-src="posts[(n - 1) * 3 + i - 1].post_picture"
                  height="290"
                  width="290"
                  :src="posts[(n - 1) * 3 + i - 1].post_picture"
                >
                  <v-card
                    v-if="hover"
                    height="290"
                    width="290"
                    style="background: rgba(0, 0, 0, 0.3)"
                    justify="center"
                  >
                    <v-container fill-height>
                      <v-row justify="center" align="center">
                        <p class="text-center white--text text-subtitle-1">
                          <v-icon color="white" class="mr-1">mdi-heart</v-icon
                          >{{ posts[(n - 1) * 3 + i - 1].post_likes
                          }}<v-icon class="mr-1 ml-7" color="white" size="21"
                            >mdi-comment</v-icon
                          >{{ posts[(n - 1) * 3 + i - 1].post_comments.length }}
                        </p>
                      </v-row>
                    </v-container>
                  </v-card>
                </v-img></v-hover
              >
            </template>
            <v-card height="800" class="mb-1" style="background-color: black">
              <v-row no-gutters>
                <v-col md="8" align="center">
                  <v-img
                    contain
                    alt="post picture"
                    :lazy-src="posts[(n - 1) * 3 + i - 1].post_picture"
                    width="1000"
                    height="800"
                    :src="posts[(n - 1) * 3 + i - 1].post_picture"
                  ></v-img
                ></v-col>

                <v-col>
                  <v-sheet
                    class="mt-n3"
                    height="662"
                    style="background-color: white"
                  >
                    <v-row class="mx-3">
                      <v-avatar
                        size="35"
                        class="mr-3 mt-5"
                        style="border: 2px solid pink; padding: 19px"
                        ><img
                          :src="posts[(n - 1) * 3 + i - 1].profile_picture"
                          alt="profile_pic"
                      /></v-avatar>
                      <h4 class="text-subtitle-2 mt-8">
                        {{ posts[(n - 1) * 3 + i - 1].username }} - Following
                      </h4>
                    </v-row>
                    <v-divider class="mt-5"></v-divider>
                    <v-row class="mx-3">
                      <v-avatar
                        size="35"
                        class="mr-3 mt-5"
                        style="border: 2px solid pink; padding: 19px"
                        ><img
                          :src="posts[(n - 1) * 3 + i - 1].profile_picture"
                          alt="profile_pic"
                      /></v-avatar>
                      <h4 class="text-subtitle-2 mt-8">
                        {{ posts[(n - 1) * 3 + i - 1].username }}
                      </h4>
                      <p
                        class="text-body-2 mx-2 my-8"
                        style="padding-top: 1.5px"
                      >
                        {{ posts[(n - 1) * 3 + i - 1].post_description }}
                      </p>
                    </v-row>
                    <v-row
                      v-for="comment in posts[(n - 1) * 3 + i - 1]
                        .post_comments"
                      :key="`${comment}`"
                      class="mx-5"
                    >
                      <h4 class="text-subtitle-2">
                        {{ comment.username }}
                      </h4>
                      <p class="text-body-2 mx-2" style="padding-top: 1.5px">
                        {{ comment.comment }}
                      </p>
                    </v-row>
                  </v-sheet>
                  <v-sheet
                      class="mt-0"
                      height="150"
                      style="background-color: white"
                    >
                      <v-divider class="py-3"></v-divider>
                      <v-row class="mx-5" justify="space-between">
                        <v-icon size="30" color="black"
                          >mdi-heart-outline</v-icon
                        >
                        <v-icon size="30" color="black"
                          >mdi-bookmark-outline</v-icon
                        >
                      </v-row>
                      <v-row class="mx-5 mt-5">
                        <h4 class="text-subtitle-2">{{ post_likes }} likes</h4>
                      </v-row>
                    <v-text-field
                    class="ml-5 mr-5 mt-6"
                      v-model="message2"
                      
                      label="Comment..."
                      clearable
                    ></v-text-field>
                    </v-sheet>
                </v-col>
              </v-row>
            </v-card>
          </v-dialog>
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
    posts: [
      {
        username: "Usuario",
        profile_picture:
          "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        post_picture: "https://wallpaperaccess.com/full/31193.jpg",
        post_likes: 200,
        post_description: "Usuario Insta life lol lorem ipsum",
        post_comments: [
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
        ],
        date_created: "",
      },
      {
        username: "Usuario",
        profile_picture:
          "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        post_picture: "https://wallpapercave.com/wp/wp4576169.jpg",
        post_likes: 200,
        post_description: "Usuario Insta life lol lorem ipsum",
        post_comments: [
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
        ],
        date_created: "",
      },
      {
        username: "Usuario",
        profile_picture:
          "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        post_picture:
          "https://us.123rf.com/450wm/kostsov/kostsov1906/kostsov190600026/126080344-modern-showcase-with-empty-space-on-pedestal-on-blue-background-3d-rendering-.jpg?ver=6",
        post_likes: 200,
        post_description: "Usuario Insta life lol lorem ipsum",
        post_comments: [
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
        ],
        date_created: "",
      },
      {
        username: "Usuario",
        profile_picture:
          "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        post_picture: "https://wallpaperaccess.com/full/1269989.jpg",
        post_likes: 200,
        post_description: "Usuario Insta life lol lorem ipsum",
        post_comments: [
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
        ],
        date_created: "",
      },
      {
        username: "Usuario",
        profile_picture:
          "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        post_picture:
          "https://us.123rf.com/450wm/kostsov/kostsov1906/kostsov190600026/126080344-modern-showcase-with-empty-space-on-pedestal-on-blue-background-3d-rendering-.jpg?ver=6",
        post_likes: 200,
        post_description: "Usuario Insta life lol lorem ipsum",
        post_comments: [
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
        ],
        date_created: "",
      },
      {
        username: "Usuario",
        profile_picture:
          "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        post_picture: "https://wallpaperaccess.com/full/31193.jpg",
        post_likes: 200,
        post_description: "Usuario Insta life lol lorem ipsum",
        post_comments: [
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
        ],
        date_created: "",
      },
      {
        username: "Usuario",
        profile_picture:
          "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        post_picture:
          "https://us.123rf.com/450wm/kostsov/kostsov1906/kostsov190600026/126080344-modern-showcase-with-empty-space-on-pedestal-on-blue-background-3d-rendering-.jpg?ver=6",
        post_likes: 200,
        post_description: "Usuario Insta life lol lorem ipsum",
        post_comments: [
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
        ],
        date_created: "",
      },
      {
        username: "Usuario",
        profile_picture:
          "https://images.pexels.com/photos/1034662/pexels-photo-1034662.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
        post_picture:
          "https://images.pexels.com/photos/1034662/pexels-photo-1034662.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
        post_likes: 200,
        post_description: "Usuario Insta life lol lorem ipsum",
        post_comments: [
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
        ],
        date_created: "",
      },
      {
        username: "Usuario",
        profile_picture:
          "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
        post_picture:
          "https://cdn.pixabay.com/photo/2016/05/05/02/37/sunset-1373171__480.jpg",
        post_likes: 200,
        post_description: "Usuario Insta life lol lorem ipsum",
        post_comments: [
          { username: "Elver", comment: "So cool, where was this taken?" },
          {
            username: "Mateobv07",
            comment: "Lorem impsum xasxs csdc wewsa leasd cexer",
          },
        ],
        date_created: "",
      },
    ],
    followers: 243,
    following: 324,
    user_real_name: "Real name",
    username: "User",
    user_description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin convallis iaculis urna, id lobortis tortor vulputate at. Sed luctus, massa sed euismod gravida, ex",
  }),
};
</script>
