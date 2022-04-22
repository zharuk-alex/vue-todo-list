<template>
  <v-app>
    <div class="d-flex align-center justify-center" style="height: 100vh">
      <HomeContent />
    </div>
  </v-app>
</template>

<script>
import HomeContent from "@/components/HomeContent.vue";

export default {
  name: "HomeView",
  components: {
    HomeContent,
  },
};
</script>
