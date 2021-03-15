<template>
  <v-app>
    <v-main>
      <AppWindow/>
    </v-main>
  </v-app>
</template>

<script>
import AppWindow from './components/AppWindow';

export default {
  name: 'App',
  components: {
    AppWindow,
  },
  data: () => ({
    //
  }),
};
</script>
