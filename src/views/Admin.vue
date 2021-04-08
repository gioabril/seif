<template>
  <div class="admin general-container">
    <v-container>
      <v-layout row wrap justify-center align-center>
        <v-flex xs12 class="cont-title">
          <span>Url ruta / completa</span>
        </v-flex>
      </v-layout>
      <v-layout row wra>
        <v-flex xs12>
          <tabla-comp />
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>
<script>

import tablaComp from '@/components/tabla-comp.vue'

export default {
  components:{
    tablaComp,
  }
}
</script>

<style lang="scss" scoped>
@import './admin.scss';
@import '../sass/globals.scss';
</style>
