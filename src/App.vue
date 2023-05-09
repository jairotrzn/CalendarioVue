<template>
  <v-app>
    <calendario/>
  </v-app>
</template>

<script>

import Calendario from './components/Calendario.vue';
export default {
  components: { Calendario },
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
