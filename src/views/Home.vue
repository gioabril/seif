<template>
  <div class="home general-container">
    <v-container>
      <v-layout row wrap justify-center align-center>
        <v-flex xs12 class="sect-button">
          <router-link to="/admin">
            <v-btn color="#f0bc5e" v-bind="attrs" v-on="on">Añadir material de apoyo</v-btn>
          </router-link>
        </v-flex>
        <v-flex xs12 class="sect-title">
          <h2>Nuestros Productos</h2>
        </v-flex>
      </v-layout>
      <v-layout row wrap justify-center align-center class="container-items">
        <v-flex xs12 md4 sm4 v-for="(item, i) in items" :key="'item'+i" class="item animated flipInY" :class="'dura-'+i">
          <div class="container-item">
            <div class="icon-item">
              <img :src="require('@/assets/icons/'+item.imgurl+'')" alt="">
            </div>
            <p>{{item.tituloitem}}</p>
            <v-btn class="item-btn" color="orange" v-bind="attrs" v-on="on">ver</v-btn>
          </div>
        </v-flex>
      </v-layout>
    </v-container>

  </div>

</template>
<script>
export default {
  name: 'Home',
  data: () => ({
    items:[
      {
        imgurl:'007-code.svg',
        tituloitem:'Seif',
      },
      {
        imgurl:'013-hacker.svg',
        tituloitem:'Seif módulos',
      },
      {
        imgurl:'020-script.svg',
        tituloitem:'Controller',
      },
      {
        imgurl:'027-web-design.svg',
        tituloitem:'Visitantes robustos',
      },
      {
        imgurl:'006-browser.svg',
        tituloitem:'PTT',
      },
      {
        imgurl:'016-machine.svg',
        tituloitem:'Controlpharm',
      },
    ]
  }),
}
</script>

<style lang="scss" scoped>
@import './home.scss';
@import '../sass/globals.scss';
</style>