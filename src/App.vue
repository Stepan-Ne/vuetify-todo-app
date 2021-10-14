<template>
  <v-app id="inspire">
<navbar :drawer="drawer"/>

<appbar @drawer="clickDrawer"/>

    <!-- <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Application</v-toolbar-title>
    </v-app-bar> -->

    <v-main>
    
    <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Navbar from "@/components/Navbar.vue";
import Appbar from "@/components/Appbar.vue";


@Component({
  components: {
    Navbar, 
    Appbar
  }
})
export default class App extends Vue {
  public  drawer: boolean =  false;
  clickDrawer() {
    this.drawer = !this.drawer;
  }
}
</script>
