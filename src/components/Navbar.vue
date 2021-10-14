<template>
 <v-navigation-drawer 
 app
 :value="localValue"
 @click="drawerClick"
 >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6">
            Vuetify Todo
          </v-list-item-title>
          <v-list-item-subtitle>
            Best Todo Ever!
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
          :to="item.to"
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
</template>

<script lang="ts">
 import {Component, Watch, Prop, Vue} from "vue-property-decorator";

interface Item {
  title: string
  icon: string
  to: string
}
@Component
 export default class Navbar extends Vue {
@Prop() readonly drawer!: boolean

public   items: Item[] = [
          { title: 'Todo', icon: 'mdi-format-list-checks', to: '/' },
          { title: 'About', icon: 'mdi-help-box', to: '/about' },
        ]
        public localValue: any = null;

mounted() {
  this.assignLocalValue()
}
@Watch('drawer')
changeDrawer() {
  this.assignLocalValue()
}
assignLocalValue() {
  this.localValue = this.drawer;
}
drawerClick() {
  this.$emit("input", !this.localValue)
}
 }
</script>
