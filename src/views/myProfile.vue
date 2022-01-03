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
          <v-hover v-slot="{ hover }">
            <v-img
              :class="{ 'on-hover': hover }"
              @click="viewPost(posts[(n - 1) * 3 + i - 1])"
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
            </v-img>
          </v-hover>
        </v-col>
      </v-row>
      <v-dialog
        v-model="dialog"
        max-width="1400"
        @click:outside="(dialog = false), (show_tags = false)"
      >
        <v-card height="800" class="mb-1" style="background-color: black">
          <v-row no-gutters>
            <v-col md="8" align="center">
              <v-img
                @click="show_tags = !show_tags"
                contain
                alt="post picture"
                :lazy-src="postView.post_picture"
                width="1000"
                height="800"
                :src="postView.post_picture"
              >
                <v-container v-if="show_tags" fill-height>
                  <v-row justify="center" align="center">
                    <v-sheet
                      v-for="postTag in tagz"
                      :key="postTag"
                      color="black"
                      height="30"
                      class="ma-3 px-2 rounded-lg"
                    >
                      <p class="text-center white--text text-subtitle-2 pt-1">
                        {{ postTag }}
                      </p>
                    </v-sheet>
                  </v-row>
                </v-container>
              </v-img></v-col
            >

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
                    ><img :src="postView.profile_picture" alt="profile_pic"
                  /></v-avatar>
                  <h4 class="text-subtitle-2 mt-8">
                    {{ postView.username }} - Following
                  </h4>
                </v-row>
                <v-divider class="mt-5"></v-divider>
                <v-row class="mx-3">
                  <v-avatar
                    size="35"
                    class="mr-3 mt-5"
                    style="border: 2px solid pink; padding: 19px"
                    ><img :src="postView.profile_picture" alt="profile_pic"
                  /></v-avatar>
                  <h4 class="text-subtitle-2 mt-8">
                    {{ postView.username }}
                  </h4>
                  <p class="text-body-2 mx-2 my-8" style="padding-top: 1.5px">
                    {{ postView.post_description }}
                  </p>
                </v-row>
                <v-row
                  v-for="comment in postView.post_comments"
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
                  <v-icon
                    @click="liked = !liked"
                    v-if="!liked"
                    size="30"
                    color="black"
                    >mdi-heart-outline</v-icon
                  >
                  <v-icon
                    @click="liked = !liked"
                    v-if="liked"
                    size="30"
                    color="red accent-2"
                    >mdi-heart</v-icon
                  >
                  <v-icon
                    @click="saved = !saved"
                    v-if="saved"
                    size="30"
                    color="black"
                    >mdi-bookmark</v-icon
                  >
                  <v-icon
                    @click="saved = !saved"
                    v-if="!saved"
                    size="30"
                    color="black"
                    >mdi-bookmark-outline</v-icon
                  >
                </v-row>
                <v-row class="mx-5 mt-5">
                  <h4 class="text-subtitle-2">
                    {{ postView.post_likes }} likes
                  </h4>
                </v-row>
                <v-text-field
                  class="ml-5 mr-5 mt-6"
                  v-model="comment"
                  label="Comment..."
                  clearable
                ></v-text-field>
              </v-sheet>
            </v-col>
          </v-row>
        </v-card>
      </v-dialog>
    </v-container>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Profile",

  components: {
    //
  },
  data: () => ({
    dialog: false,
    postView: {},
    comment: "",
    tagz: ["lol", "mateo"],
    show_tags: false,
    liked: false,
    saved: false,
    posts: [],
    followers: 243,
    following: 324,
    user_real_name: "Real name",
    username: "User",
    user_description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin convallis iaculis urna, id lobortis tortor vulputate at. Sed luctus, massa sed euismod gravida, ex",
  }),
  created() {
    this.getUserInfo();
    this.getPosts();
  },
  methods: {
    show_tag() {
      this.show_tags = !this.show_tags;
    },
    viewPost(post) {
      this.postView = {};
      this.postView = post;
      this.dialog = true;
    },
    getUserInfo() {
      var vueinstance = this;
      axios({
        method: "GET",
        url: "http://127.0.0.1:8000/account/myprofile/",
        headers: {
          Authorization: "Token b0f55c48c8631f081a7319920972fc6c1da4b697",
        },
      })
        .then(function (response) {
          console.log(response.data);
          var user_object = response.data
          vueinstance.username = user_object.user.username
          vueinstance.user_real_name = user_object.user.real_name 
          vueinstance.description = user_object.description
        })
        .catch(function (error) {
          console.log(error);
        });
    },

    getPosts() {
      var vueinstance = this;
      var unparsed_posts;
      var current_post;
      var parsed_comments;
      axios({
        method: "GET",
        url: "http://127.0.0.1:8000/post/myPosts/",
        headers: {
          Authorization: "Token b0f55c48c8631f081a7319920972fc6c1da4b697",
        },
      })
        .then(function (response) {
          console.log(response.data);
          unparsed_posts = response.data;
          vueinstance.posts = [];
          for (let i = 0; i < unparsed_posts.length; i++) {
            parsed_comments = [];
            for (let n = 0; n < unparsed_posts[i].comments.length; n++) {
              var parsing_comment = {
                username: unparsed_posts[i].comments[n].username,
                comment: unparsed_posts[i].comments[n].comment,
              };
              parsed_comments.push(parsing_comment);
            }
            current_post = {
              username: vueinstance.username,
              profile_picture:
                "https://images.unsplash.com/photo-1541701494587-cb58502866ab?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MXx8fGVufDB8fHx8&w=1000&q=80",
              post_picture: "http://127.0.0.1:8000" + unparsed_posts[i].image,
              post_likes: unparsed_posts[i].likes,
              post_description: unparsed_posts[i].description,
              post_comments: parsed_comments,
              date_created: "",
              post_tags: [],
            };
            vueinstance.posts.push(current_post);
          }
          console.log(vueinstance.posts);
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
};
</script>
