<template>
  <v-app>
    <v-main>
      <HomeContent />
    </v-main>
  </v-app>
</template>

<script>
  import HomeContent from './components/HomeContent.vue';
  export default {
    name: 'App',
    components: {
      HomeContent,
    },
  };
</script>
<style>
  body {
    overflow: hidden;
  }
  .v-application--wrap {
    background-color: #666afb;
  }
</style>
