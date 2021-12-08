<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-card height="120" max-width="620" min-width="620" elevation="1">
          <v-row >
            <v-col
              v-for="i in story_images"
              :key="`${i}`"
              class="text-center"
            >
           
              <v-avatar size="60" style="border: 2px solid pink;padding: 32px;" 
                ><img src="../assets/background.jpg" alt="profile_pic"
              /></v-avatar>
              <p class="caption">namedds</p>
              
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",
  

  data: () => ({
    story_images: 6,
  }),
};
</script>
