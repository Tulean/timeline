<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center"></div>
    </v-app-bar>
    <v-content>
      <timeline />
    </v-content>
  </v-app>
</template>

<script>
import timeline from "./components/timeline";

export default {
  name: "App",

  components: {
    timeline
  },

  data: () => ({
    //
  })
};
</script>
