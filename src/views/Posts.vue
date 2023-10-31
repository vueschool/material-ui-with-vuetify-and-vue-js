<script setup lang="ts">
import { ref } from "vue";
import { VDataTable } from "vuetify/labs/VDataTable";
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
</script>
<template>
  <div>
    <h1>Posts</h1>
    <v-text-field
      v-model="search"
      append-icon="mdi-magnify"
      label="Search"
      single-line
      hide-details
    ></v-text-field>

    <v-data-table
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
    ></v-data-table>
  </div>
</template>
