<template>
  <div class="app-view">
    <h1>Menu</h1>
    <v-container fluid>
      <v-row>
        <v-col v-for="n in 9" :key="n" class="d-flex child-flex" cols="4">
          <v-card flat tile class="d-flex">
            <v-img
              :src="`https://picsum.photos/500/300?image=${n * 5 + 10}`"
              :lazy-src="`https://picsum.photos/10/6?image=${n * 5 + 10}`"
              aspect-ratio="1"
              class="grey lighten-2"
            >
              <template v-slot:placeholder>
                <v-row class="fill-height ma-0" align="center" justify="center">
                  <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                </v-row>
              </template>
            </v-img>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import DatabaseMixin from "@/mixins/DatabaseMixin.vue";

export default {
  name: "Menu",
  mixins: [DatabaseMixin]
};
</script>

<style>
.menu {
  height: 100%;
  width: 100%;
}
</style>