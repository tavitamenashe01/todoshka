<template>
  <q-layout view="hHh lpR fFf">
    <q-header  elevated class="bg-secondary">
      <q-toolbar color="puple">
        <q-toolbar-title class="absolute-center">My todoshka-dushka</q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>

export default {
  name: "Layout",
  data() {
    return {
    };
  }
};
</script>

<style >
/* body {
  background: #000;
} */
</style>
