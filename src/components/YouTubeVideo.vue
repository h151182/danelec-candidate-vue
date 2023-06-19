<template>
  <v-list-item link :href="linkUrl" target="_blank">
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
  </v-list-item>
</template>

<script lang="ts">
import { Component, Model, Vue } from "vue-property-decorator";
import config from "@/config";
// import actions from "@/actions";

@Component({ name: "YouTubeVideo" })
export default class YouTubeVideo extends Vue {
  @Model() video!: any;

  title: any = "";
  imageUrl: any = "";
  description: any = "";
  id: any = "";
  linkUrl: any = "";

// replaced typo in imageUrl from "src" to "url"
  mounted() {
    this.title = this.video.snippet.title;
    this.imageUrl = this.video.snippet.thumbnails.default.url;
    this.description = this.video.snippet.description;
    this.id = this.video.id.videoId;
    this.linkUrl = config.youtubeWatchBaseUrl + this.id;
  }

  // viewEmbedded() {
  //     var videoId = this.id.substring(this.id.lastIndexOf("/") + 1);
  //     var embedUrl = config.youtubeEmbedBaseUrl + videoId;
  //     actions.showVideoModal.dispatch({src: embedUrl, height: 400, width: 300});
  // }
}
</script>
