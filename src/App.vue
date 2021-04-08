<template>
  <div id="app">
    <v-app>
    <div id="nav">
      <h2>Centro de Ayuda SEIF</h2>
      <!-- <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> -->
    </div>
    <router-view/>
    <!-- <nav-bar/> -->
    </v-app>
  </div>
</template>
<script>
// import navBar from '@/components/nav-bar.vue'
export default {
  name: "App",
  // components:{
  //   navBar
  // }
}
</script>

<style lang="scss" >
@import './sass/globals.scss';

#app {
  text-align: center;
  color: #2c3e50;
  width: 100%;
  padding: 10px!important;
  font-size: 16px;
  font-family: FontBase-Regular;
  text-align: center;

}

#nav {
  padding: 30px;
  text-align: center;
  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
/********************  FONTS ********************/
/* Las fuentes se cargan acá porque se tiene acceso a los recursos que están en assets*/

@font-face {
  font-family: FontBase-Black;
  src: url("./assets/fonts/SourceSansPro-Black.ttf");
}
@font-face {
  font-family: FontBase-BlackItalic;
  src: url("./assets/fonts/SourceSansPro-BlackItalic.ttf");
}
@font-face {
  font-family: FontBase-Regular;
  src: url("./assets/fonts/SourceSansPro-Regular.ttf");
}
@font-face {
  font-family: FontBase-Bold;
  src: url("./assets/fonts/SourceSansPro-Bold.ttf");
}
@font-face {
  font-family: FontBase-BoldItalic;
  src: url("./assets/fonts/SourceSansPro-BoldItalic.ttf");
}
@font-face {
  font-family: FontBase-SemiBold;
  src: url("./assets/fonts/SourceSansPro-SemiBold.ttf");
}
@font-face {
  font-family: FontBase-Light;
  src: url("./assets/fonts/SourceSansPro-Light.ttf");
}

// SourceSansPro-ExtraLight.ttf
// SourceSansPro-ExtraLightItalic.ttf
// SourceSansPro-Italic.ttf
// SourceSansPro-LightItalic.ttf
// SourceSansPro-SemiBoldItalic.ttf

</style>
