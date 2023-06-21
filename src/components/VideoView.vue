<template>
 <v-sheet
    width="auto"
    >
      <v-card>
       <iframe width="560" height="315" :src="embedUrl" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
      </v-card>
    </v-sheet>
  
</template>

<script lang="ts">
import { Component, Model, Vue } from "vue-property-decorator";

@Component({ name: "VideoView" })
export default class VideoView extends Vue {
  @Model() showModal!: boolean;
  @Model() embedUrl: any; 


}
</script>