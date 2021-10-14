<template>
  <div class="home pa-6">
    <h2>Todo List</h2>
    <v-text-field
    v-model="newTextTask"
      label="Outlined"
      placeholder="Placeholder"
      outlined
      clearable
      append-icon="mdi-plus"
      @click:append="addTask"
      @keyup.enter="addTask"
    ></v-text-field>
    <v-list flat>
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="onClickItem(task.id)"
          :class="{ 'blue lighten-5': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title>{{ task.task }}</v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn
                @click.stop="removeItem(task.id)"
                fab
                dark
                small
                color="primary lighten-2"
              >
                <v-icon dark>
                  mdi-minus
                </v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
// import HelloWorld from '../components/Navbar.vue'
@Component
export default class Todo extends Vue {
  public tasks: any = [
    { id: 1, task: "One", done: false },
    { id: 2, task: "Two", done: false },
  ];
public newTextTask: string = ''
  onClickItem(id: number) {
    let t = this.tasks.filter((task: any) => task.id === id)[0];
    t.done = !t.done;
  }
  removeItem(id: number) {
    this.tasks = this.tasks.filter((task: any) => task.id !== id);
  }
  addTask() {
    if (this.newTextTask.trim()) {
    let nt = {id: Date.now(), done: false, task: this.newTextTask}
    this.tasks = [nt, ...this.tasks]
    this.newTextTask = ''
    }

  }
}
</script>

<style lang="sass">

</style>
