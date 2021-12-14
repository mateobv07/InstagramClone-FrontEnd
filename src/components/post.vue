<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-card
          height="auto"
          max-width="620"
          min-width="620"
          elevation="0"
          style="border: 0.1px solid #b6bab7"
        >
          <v-card-title>
            <v-avatar
              size="35"
              class="mr-3 my-n2"
              style="border: 2px solid pink; padding: 19px"
              ><img :src="profile_picture" alt="profile_pic"
            /></v-avatar>
            <h4 class="text-subtitle-2">{{ username }}</h4>
          </v-card-title>

          <v-divider></v-divider>
          <v-img
          @click="show_tags = !show_tags"
            :lazy-src="post_picture"
            max-width="auto"
            :src="post_picture"
            alt="post picture"
          >
           <v-container v-if="show_tags" fill-height>
                      <v-row justify="center" align="center">
                      <v-sheet v-for="tag in post_tags" :key="tag" color="black" height="30" class="ma-3 px-2 rounded-lg">
                        <p  class="text-center white--text text-subtitle-2 pt-1">
                          {{tag}}
                        </p>
                        </v-sheet>
                      </v-row>
                    </v-container>
          </v-img>
          <v-divider class="pb-6"></v-divider>
          <v-row class="mx-4" justify="space-between">
            <v-icon @click="liked = !liked" v-if="!liked" size="30" color="black">mdi-heart-outline</v-icon>
            <v-icon @click="liked = !liked" v-if="liked" size="30" color="red accent-2">mdi-heart</v-icon>
            <v-icon @click="saved = !saved" v-if="saved" size="30" color="black">mdi-bookmark</v-icon>
            <v-icon @click="saved = !saved" v-if="!saved" size="30" color="black">mdi-bookmark-outline</v-icon>
          </v-row>
          <v-row class="mx-4 mt-6">
            <h4 class="text-subtitle-2">{{ post_likes }} likes</h4>
          </v-row>
          <v-row class="mx-4 mt-4">
            <h4 class="text-subtitle-2">{{ username }}</h4>
            <p class="text-body-2 mx-1" style="padding-top: 1.5px">
              {{ post_description }}
            </p>
          </v-row>
          <v-row class="ml-n1 mt-0">
            <v-dialog v-model="viewPost" max-width="1400">
              <template v-slot:activator="{ on, attrs }">
                <v-btn text v-bind="attrs" v-on="on" height="20">
                  <p class="text-body-2 mt-3" style="opacity: 65%">
                    View {{ post_comments.length }} comments
                  </p>
                </v-btn>
              </template>
              <v-card height="800" class="mb-1" style="background-color: black">
                <v-row no-gutters>
                  <v-col md="8" align="center">
                    <v-img
                    @click="show_tags = !show_tags"
                      contain
                      alt="post picture"
                      :lazy-src="post_picture"
                      width="1000"
                      height="800"
                      :src="post_picture"
                    >
                    <v-container v-if="show_tags" fill-height>
                      <v-row justify="center" align="center">
                      <v-sheet v-for="tag in post_tags" :key="tag" color="black" height="30" class="ma-3 px-2 rounded-lg">
                        <p  class="text-center white--text text-subtitle-2 pt-1">
                          {{tag}}
                        </p>
                        </v-sheet>
                      </v-row>
                    </v-container>
                    </v-img
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
                          ><img :src="profile_picture" alt="profile_pic"
                        /></v-avatar>
                        <h4 class="text-subtitle-2 mt-8">
                          {{ username }} - Following
                        </h4>
                      </v-row>
                      <v-divider class="mt-5"></v-divider>
                      <v-row class="mx-3">
                        <v-avatar
                          size="35"
                          class="mr-3 mt-5"
                          style="border: 2px solid pink; padding: 19px"
                          ><img :src="profile_picture" alt="profile_pic"
                        /></v-avatar>
                        <h4 class="text-subtitle-2 mt-8">{{ username }}</h4>
                        <p
                          class="text-body-2 mx-2 my-8"
                          style="padding-top: 1.5px"
                        >
                          {{ post_description }}
                        </p>
                      </v-row>
                      <v-row
                        v-for="comment in post_comments"
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
          </v-row>
          <v-row class="mx-4 mt-3 mb-0">
            <p class="BUTTON" style="opacity: 65%; font-size: x-small">
              HACE 4 HORAS
            </p>
          </v-row>
          <v-divider></v-divider>
          <v-row class="mx-4 pt-0 mb-n6">
            <v-icon size="24" color="black" class="mt-n3"
              >mdi-comment-outline</v-icon
            >
            <v-text-field
              placeholder="Add Comment"
              class="mt-4 text-body-2"
              solo
              flat
            ></v-text-field>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Post",
  data: () => ({
    show_tags: false,
    viewPost: false,
    liked: false,
    saved: false,
  }),
  props: {
    username: String,
    profile_picture: String,
    post_picture: String,
    post_likes: Number,
    post_description: String,
    post_comments: Array,
    post_tags: Array,
  },
  
};
</script>
