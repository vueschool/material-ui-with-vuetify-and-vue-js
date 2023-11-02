<script setup lang="ts">
import { ref } from "vue";
import { VDataTable } from "vuetify/labs/VDataTable";
import PostForm from "@/components/PostForm.vue";
import { refAutoReset } from "@vueuse/core";
const posts = ref([
  { title: "Post 1", author: "Fred" },
  { title: "Post 2", author: "Wilma" },
  { title: "Post 3", author: "Barney" },
  { title: "Post 4", author: "Bam-Bam" },
  { title: "Post 5", author: "Fred" },
  { title: "Post 6", author: "Wilma" },
  { title: "Post 7", author: "Barney" },
  { title: "Post 8", author: "Bam-Bam" },
  { title: "Post 9", author: "Fred" },
  { title: "Post 10", author: "Wilma" },
  { title: "Post 11", author: "Barney" },
  { title: "Post 12", author: "Bam-Bam" },
]);

const selected = ref([]);
const search = ref("");
const postForm = ref();

const postSaved = refAutoReset(false, 4000);

function handleClickOutside() {
  selected.value = [];
}

type densities = "default" | "compact" | "comfortable";
const tableDensity = ref<densities>("default");
function handleResize() {
  let density: densities = "default";
  if (window.innerHeight < 800) density = "comfortable";
  if (window.innerHeight < 600) density = "compact";
  tableDensity.value = density;
}
</script>
<template>
  <div>
    <v-alert
      variant="tonal"
      type="success"
      closable
      title="Post Updated"
      v-model="postSaved"
    />

    <!-- <v-snackbar v-model="postSaved" :timeout="4000">
      <div class="d-flex align-center">
        <v-icon icon="mdi-check-circle" class="text-green pr-3"></v-icon>
        Post Saved!
      </div>
    </v-snackbar> -->

    <h1>Posts</h1>
    <v-text-field
      v-model="search"
      append-icon="mdi-magnify"
      label="Search"
      single-line
      hide-details
    ></v-text-field>

    <v-data-table
      v-click-outside="handleClickOutside"
      v-resize="handleResize"
      :headers="[
        {
          title: 'Post Title',
          align: 'start',
          sortable: false,
          key: 'title',
        },
        { title: 'Author', align: 'end', key: 'author' },
      ]"
      :items="posts"
      show-select
      item-value="title"
      v-model="selected"
      :search="search"
      :density="tableDensity"
    >
      <template #item.title="{ item }">
        <v-dialog fullscreen>
          <template v-slot:activator="{ props }">
            <button v-bind="props" v-ripple class="pa-3">
              {{ item.title }}
            </button>
          </template>

          <template v-slot:default="{ isActive }">
            <v-card title="Edit Post">
              <v-card-text>
                <PostForm
                  ref="postForm"
                  :post="item"
                  @submit="
                    isActive.value = false;
                    postSaved = true;
                  "
                />
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>

                <v-btn text="Cancel" @click="isActive.value = false"></v-btn>

                <v-btn
                  color="blue"
                  variant="flat"
                  text="Save Post"
                  @click="postForm.submit()"
                ></v-btn>
              </v-card-actions>
            </v-card>
          </template>
        </v-dialog>
      </template>
    </v-data-table>
  </div>
</template>
