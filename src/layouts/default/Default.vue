<template>
  <v-layout class="rounded rounded-md">
    <v-app-bar title="Application bar">
      <template #append>
        <v-menu>
          <template v-slot:activator="{ props }">
            <v-avatar v-bind="props" size="50" color="blue">
              <span>DK</span>
            </v-avatar>
          </template>
          <v-list>
            <v-list-item
              v-for="(item, index) in ['Profile', 'Settings', 'Logout']"
              :key="index"
              :value="index"
            >
              <v-list-item-title>{{ item }}</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </template>
    </v-app-bar>

    <v-navigation-drawer>
      <v-list>
        <v-list-item title="Navigation drawer"></v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main
      class="d-flex align-center justify-center"
      style="min-height: 300px"
    >
      <router-view></router-view>
    </v-main>
  </v-layout>
</template>
