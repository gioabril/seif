<template>
  <div class="home">
    <v-container >
      <v-layout row wrap>
        <v-flex xs12>
          <v-btn color="orange" v-bind="attrs" v-on="on">Añadir material de apoyo</v-btn>
        </v-flex>
        <v-flex xs12 >
          <h2>Nuestros Productos</h2>
        </v-flex>
      </v-layout>
      <v-layout row wrap justify-center align-center class="container-items">
        <v-flex xs12 md4 sm4 v-for="(item, i) in items" :key="'item'+i" class="item">
          <div class="icon-item">
            <!-- <img :src="required('@/assets/icons/'+item.imgurl+'')" alt=""> -->
          </div>
          <p>{{item.tituloitem}}</p>
          <v-btn color="orange" v-bind="attrs" v-on="on">ver</v-btn>
        </v-flex>
      </v-layout>
    </v-container>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
  
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  // components: {
  //   HelloWorld
  // }
  data: () => ({
    items:[
      {
        imgurl:'006-browser.svg',
        tituloitem:'Seif',
      },
      {
        imgurl:'006-browser.svg',
        tituloitem:'Seif módulos',
      },
      {
        imgurl:'006-browser.svg',
        tituloitem:'Controller',
      },
      {
        imgurl:'006-browser.svg',
        tituloitem:'Visitantes robustos',
      },
      {
        imgurl:'006-browser.svg',
        tituloitem:'PTT',
      },
      {
        imgurl:'006-browser.svg',
        tituloitem:'Controlpharm',
      },
    ]
  }),
  created() {

  },
}
</script>

<style lang="scss" scoped>
@import './home.scss';

</style>