<template>
  <v-list-item @click="showModal = !showModal">
    <v-list-item-avatar size="100">
  <!--
  replaced typo imageSrc with imageUrl
  -->
      <v-img :src="imageUrl"></v-img>
    </v-list-item-avatar>

    <v-list-item-content>
      <v-list-item-title>{{ title }}</v-list-item-title>
      <v-list-item-subtitle>{{ description }}</v-list-item-subtitle>
    </v-list-item-content>
    <VideoView v-if="showModal" v-model="embedUrl"/>
  </v-list-item>
  
</template>

<script lang="ts">
import { Component, Model, Vue } from "vue-property-decorator";
import VideoView from "@/components/VideoView.vue"
import config from "@/config";

@Component({ 
  name: "YouTubeVideo", 
  components: { VideoView }})
export default class YouTubeVideo extends Vue {
  @Model() video!: any;

 showModal: boolean = false;
  title: any = "";
  imageUrl: any = "";
  description: any = "";
  id: any = "";
  linkUrl: any = "";
  embedUrl: any = "";

// replaced typo in imageUrl from "src" to "url"
  mounted() {
    this.title = this.video.snippet.title;
    this.imageUrl = this.video.snippet.thumbnails.default.url;
    this.description = this.video.snippet.description;
    this.id = this.video.id.videoId;
    this.linkUrl = config.youtubeWatchBaseUrl + this.id;

    // added from viewEmbedded() 
    var videoId = this.id.substring(this.id.lastIndexOf("/") + 1);
    this.embedUrl = config.youtubeEmbedBaseUrl + videoId;
  }

}
</script>
