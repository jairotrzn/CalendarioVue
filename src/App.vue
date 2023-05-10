<template>
  <v-app>
    <TableCrud/>
  </v-app>
</template>

<script>

import Calendario from './components/Calendario.vue';
import TableCrud from './components/TableCrud.vue';

export default {
  components: { Calendario,TableCrud },
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
