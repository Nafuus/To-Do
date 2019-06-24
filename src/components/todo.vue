<template>
  <v-app id="inspire">
    <v-toolbar :clipped-left="$vuetify.breakpoint.lgAndUp" color="blue darken-3" dark app fixed>
      <v-toolbar-title style="width: 300px" class="ml-0 pl-3">
        <span>To-Do</span>
      </v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-expansion-panel expand>
        <v-expansion-panel-content v-for="(todo, index) in todos">
          <template v-slot:header>
            <div>{{ todo.title }} {{ todo.id }}</div>
          </template>
          <template v-slot:actions>
            <v-icon color="error" title="Завершить" @click="removeTodo(index)">error</v-icon>
          </template>
          <v-card>
            <v-card-text class="grey lighten-3">{{ todo.description }}</v-card-text>
          </v-card>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-content>
    <v-btn fab bottom right color="#0078D7" dark fixed @click="openDialog">
      <v-icon>add</v-icon>
    </v-btn>
    <v-dialog width="800px" v-model="dialog">
      <v-card>
        <v-card-title class="grey lighten-4 py-4 title">Добавить задачу</v-card-title>
        <v-container grid-list-sm class="pa-4">
          <v-layout row wrap>
            <v-layout align-center>
              <v-text-field placeholder="Задача" v-model="todo.title"></v-text-field>
            </v-layout>
          </v-layout>
          <v-layout row wrap>
            <v-layout align-center>
              <v-text-field placeholder="Описание задачи" v-model="todo.description"></v-text-field>
            </v-layout>
          </v-layout>
        </v-container>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn flat color="primary" @click="closeDialog">отмена</v-btn>
          <v-btn flat @click="addTodo">сохранить</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      dialog: false,
      drawer: null,

      todos:[],

      todo: {
        title: '',
        description: ''
      }
    }),
    methods:{
      closeDialog() {
        this.dialog = false;
      },
      openDialog() {
        this.dialog = true;
      },

      clearInput() {
        this.todo = {
          title: '',
          description: ''
        };
      },

      addTodo(){
        this.todos.push({
          title: this.todo.title,
          description: this.todo.description,
          id: this.todo.length
        });

        this.closeDialog();
        this.clearInput();
      },
      removeTodo(index){
        this.todos.splice(index, 1);
      }
    }
  }
</script>
