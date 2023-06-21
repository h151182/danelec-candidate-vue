<template>
  <!--
  added event for @keydown.enter
  -->
  <div @keydown.enter="search">
    <v-card class="elevation-12">
      <v-toolbar color="primary" dark flat>
  <!--
  replaced typo YoutToube with YouTube
  -->
        <v-toolbar-title>YouTube Search</v-toolbar-title>
      </v-toolbar>
      <v-card-text>
        <v-text-field
          v-model="q"
          hide-details
          prepend-icon="mdi-magnify"
          single-line
          label="Find your favorite YouTube videos here"
          outlined
        ></v-text-field>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>

  <!--
  added radio group for maxResult
  -->
    <v-container fluid>
      <div>Choose number of videos</div>
    <v-radio-group inline v-model="max">
  <v-radio label="5" value=5></v-radio>
  <v-radio label="10" value=10></v-radio>
  <v-radio label="20" value=20></v-radio>
</v-radio-group>
        </v-container>

  <!--
  added @click
  -->
        <v-btn @click="search">Search</v-btn>
      </v-card-actions>
    </v-card>
    
    <v-alert type="info" v-if="v.length > 0">
      Found {{ v.length }} videos
    </v-alert>

    <v-list three-line>
      <template v-for="(item, index) in v">
        <YouTubeVideo :key="index" v-model="item.video"></YouTubeVideo>
      </template>
    </v-list>

  </div>
 
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";
import YouTubeVideo from "@/components/YouTubeVideo.vue";
import axios from "axios";
import config from "@/config";

@Component({
  name: "YouTubeSearch",
  components: { YouTubeVideo },
})
export default class YouTubeSearch extends Vue {
  q: string = "cute dog";
  r: any = null;
  v: any = [];
  max: number = 5;


//clears the video list when called 
  search() {
    this.v = []
    axios
      .get(config.youtubeBaseUrl, {
        params: {
          q: this.q,
          maxResults: this.max,
          key: config.youtubeApiKey,
          part: "snippet"
        },
      })
      .then((res) => {
        this.r = res.data;
      });
  }

//added a search on mount 
  mounted(){
  //this.search()
  }


  @Watch("r")
  Update() {
    this.r.items.forEach((item: any) => {
      this.v.push({ video: item });
    });
  }
}
</script>
