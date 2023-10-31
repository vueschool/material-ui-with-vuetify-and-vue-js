<script setup lang="ts">
import { ref } from "vue";
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
</script>
<template>
  <div>
    <h1>Posts</h1>
    <v-table :height="300" :fixed-header="true" :hover="true">
      <thead>
        <tr>
          <th class="text-left">Name</th>
          <th class="text-left">Author</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in posts" :key="item.title">
          <td>{{ item.title }}</td>
          <td>{{ item.author }}</td>
        </tr>
      </tbody>
    </v-table>
  </div>
</template>
