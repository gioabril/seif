<template>

      <!-- <router-link to="/">Home</router-link> |
      About</router-link> -->
  <div>
  <v-card class="nav-container" v-if="!$vuetify.breakpoint.xs">
    <v-navigation-drawer 
      v-model="drawer"
      :mini-variant.sync="mini"
      permanent
      width="200px"
      class="mx-auto nav-bar"
      color="#f0bc5e"
      fixed
      bottom
    >
      <v-list-item class="px-2">
        <v-list-item-avatar>
          <v-img src="https://randomuser.me/api/portraits/men/85.jpg"></v-img>
        </v-list-item-avatar>

        <v-list-item-title>Usuario Administrador</v-list-item-title>

        <v-btn icon @click.stop="mini = !mini">
          <v-icon>mdi-chevron-left</v-icon>
        </v-btn>
      </v-list-item>
      <v-divider></v-divider>
      <v-list dense>
        <v-list-item v-for="item in items" :key="item.title" link :to="item.tourl">
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </v-card>
  <div class="nav-container-hz" v-if="$vuetify.breakpoint.xs">
    <div class="icon" v-for="item in items" :key="item.title">
      <router-link :to="item.tourl">
        <v-icon>{{ item.icon }}</v-icon>
      </router-link> 
    </div>
  </div>

  </div>
</template>

<script>
  export default {
    name: 'home',
    data: () => ({
      drawer: true,
        items: [
          { title: 'Inicio', icon: 'mdi-home-city', tourl:'/' },
          { title: 'Administrar', icon: 'mdi-account', tourl:'/admin' },
          { title: 'Mi cuenta', icon: 'mdi-account-group-outline', tourl:'/admin' },
        ],
        mini: true,
    }),
  }
</script>
<style scoped lang="scss">
@import '../sass/globals.scss';

.nav-container{
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  @media screen and(max-width: 600px) {
    // display: none;
  }
}
.nav-container-hz{
  background: $color-base;
  width: 100vw;
  height: 40px;
  position: fixed;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  .icon{
    margin: 0px 10px;
    a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: $color-success;
    }
    }
  }
}
</style>