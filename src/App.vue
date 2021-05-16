<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    </v-app-bar>

    <v-main>
      <Recorder />
    </v-main>
  </v-app>
</template>

<script>
import Recorder from '@/components/Recorder'

export default {
  name: 'App',

  components: {
    Recorder
  },

  data: () => ({
    //
  }),
}
</script>