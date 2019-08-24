<template>
  <v-container class="csutom_container">
    <v-row>
      <v-col cols="3">
        <v-card max-width="500" class="mx-auto">
          <v-toolbar dark color="#3f51b5" class="custom_toolbar">
            <v-toolbar-title class="custom_toolbar_title">TODO</v-toolbar-title>
          </v-toolbar>
          <v-list class="custom_card">
            <v-list-item-group>
              <draggable class="list-group" :list="todos" group="people" @change="log">
                <template v-for="(todo, index) in todos">
                  <v-list-item :key="todo.id" class="custom_list">
                    <Todo :key="index" :data="todo" />
                  </v-list-item>
                </template>
              </draggable>
              <div class="subtitle-2 add-task" v-show="!isAdd" v-on:click="addTask">+ Add another task</div>
              <v-textarea solo name="input-5-2" label="Add content" v-show="isAdd" v-on:keyup.enter="submit" v-model="newTodoText"></v-textarea>
            </v-list-item-group>
          </v-list>
        </v-card>
      </v-col>
      <v-col cols="3">
        <v-card max-width="500" class="mx-auto">
          <v-toolbar dark color="#3f51b5" class="custom_toolbar">
            <v-toolbar-title class="custom_toolbar_title">DOING</v-toolbar-title>
          </v-toolbar>
          <v-list two-line class="custom_card">
            <v-list-item-group>
              <draggable class="list-group" :list="doings" group="people" @change="log">
                <template v-for="(todo, index) in doings">
                  <v-list-item :key="todo.id" class="custom_list">
                    <Todo :key="index" :data="todo" />
                  </v-list-item>
                </template>
              </draggable>
            </v-list-item-group>
          </v-list>
        </v-card>
      </v-col>
      <v-col cols="3">
        <v-card max-width="500" class="mx-auto">
          <v-toolbar dark color="#3f51b5" class="custom_toolbar">
            <v-toolbar-title class="custom_toolbar_title">DONE</v-toolbar-title>
          </v-toolbar>
          <v-list two-line class="custom_card">
            <v-list-item-group>
              <draggable class="list-group" :list="dones" group="people" @change="log">
                <template v-for="(todo, index) in dones">
                  <v-list-item :key="todo.id" class="custom_list">
                    <Todo :key="index" :data="todo" />
                  </v-list-item>
                </template>
              </draggable>
            </v-list-item-group>
          </v-list>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { todos, doings, dones, status } from "../data";
import Todo from "./Todo";
import draggable from "vuedraggable";

export default {
  components: {
    Todo,
    draggable
  },
  data: () => {
    return {
      todos,
      doings,
      dones,
      listsStatus: status,
      isAdd: false,
      newTodoText: ''
    };
  },
  methods: {
    submit: function(message, event){
      if (event) event.preventDefault()
      const task = {
        id: new Date().getUTCMilliseconds(),
        title: this.newTodoText
      }      
      this.isAdd = false;
      this.todos = [...this.todos, task];
      this.newTodoText = ''
    },
    addTask: function(){
      this.isAdd = true
    },
    log: function(evt) {
      window.console.log(evt);
    }
  }
};
</script>
<style >
.custom_card {
  padding: 10px 20px !important;
  background-color: #f2f2f2 !important;
}
.custom_list {
  background-color: #fff !important;
  margin: 10px 0px !important;
  border-radius: 3px;
  min-height: 40px !important;
}
.custom_toolbar {
  height: 55px !important;
}
.custom_toolbar_title {
  font-size: 1rem !important;
  font-weight: 400 !important;
}

.csutom_container {
  background-color: transparent !important;
}
.add-task {
  margin: 25px 0px 10px 0px !important;
  color: #bbb;
}
.add-task:hover {
  text-decoration-line: underline;
  cursor: pointer;
}
</style>

