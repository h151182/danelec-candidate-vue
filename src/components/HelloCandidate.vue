<template>
  <div>
    
    <v-col>
      <v-sheet class="elevation-12 pa-2">
        <v-img src="../assets/logo.svg"></v-img>
      </v-sheet>
    </v-col>
    <v-col>
      <v-card class="elevation-12">
        <v-card-title> Great! It's working </v-card-title>

        <v-card-text>
          <v-alert type="warning" border="left" elevation="2" colored-border>
            Our YouTube Search is up
            <v-icon>mdi-emoticon-cool-outline</v-icon><br />
          </v-alert>
        </v-card-text>
      </v-card>
    </v-col>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({ name: "HelloCandidate" })
export default class HelloCandidate extends Vue {}
</script>
