<template>
  <v-app-bar flat>
    <template v-slot:prepend>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
    </template>
    <v-app-bar-title>
      Bard
      <v-chip class="rounded-lg" color="primary" variant="outlined">
        Experiment
      </v-chip>
    </v-app-bar-title>
    <template v-slot:append>
      <v-btn icon="mdi-apps"></v-btn>
      <v-btn icon>
        <v-avatar>
          <v-icon icon="mdi-account-circle"></v-icon>
        </v-avatar>
      </v-btn>
    </template>
  </v-app-bar>
</template>

<script lang="ts" setup>
  //
</script>
