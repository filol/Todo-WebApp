<template id="list">
  <v-container fluid grid-list-md>
    <v-card fluid>
      <v-card-title primary class="title">
        <v-flex>
          <v-text-field label="Title" outline v-model="newTodo.title"></v-text-field>
        </v-flex>
      </v-card-title>
      <v-card-text>
        <v-flex>
          <v-textarea label="Content" v-model="newTodo.content"></v-textarea>
        </v-flex>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn class="white--text" color="red" @click="addTodo">Add</v-btn>
      </v-card-actions>
    </v-card>
    <v-layout row wrap>
      <v-flex d-flex xs12 sm6 md4 v-for="(todo,n) in todos" v-bind:key="todo.title">
        <v-card :color="todo.color">
          <v-card-title primary class="title">{{todo.title}}</v-card-title>
          <v-card-text>{{ todo.content }}</v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn icon class="white--text" @click="deleteTodo(n)">
              <v-icon>delete</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
let mycolor = [
  "blue lighten-2",
  "green lighten-2",
  "red lighten-2",
  "indigo",
  "purple",
  "deep-orange",
  "brown",
  "amber",
  "green",
  "lime",
  "teal ",
  "indigo accent-1",
  "blue darken-3  "
];
export default {
  data: () => ({
    todos: [
      {
        title: "Welcome",
        content:
          "Lorem ipsum dolor sit amet, mel at clita quando. Te sit oratio vituperatoribus, nam ad ipsum posidonium mediocritatem, explicari dissentiunt cu mea. Repudiare disputationi vim in, mollis iriure nec cu, alienum argumentum ius ad. Pri eu justo aeque torquatos.",
        color: mycolor[Math.floor(Math.random() * mycolor.length)]
      }
    ],
    newTodo: {
      title: "",
      content: "",
      color: mycolor[Math.floor(Math.random() * mycolor.length)]
    }
  }),
  methods: {
    addTodo() {
      if (!this.newTodo.title || !this.newTodo.content) return;
      this.todos.push(this.newTodo);
      this.newTodo = {
        title: "",
        content: "",
        color: mycolor[Math.floor(Math.random() * mycolor.length)]
      };
      this.saveTodo();
    },
    saveTodo() {
      let parsed = JSON.stringify(this.todos);
      localStorage.setItem("todos", parsed);
    },
    deleteTodo(x) {
      this.todos.splice(x, 1);
      this.saveTodo();
    }
  },
  mounted() {
    if (localStorage.getItem("todos")) {
      try {
        this.todos = JSON.parse(localStorage.getItem("todos"));
      } catch (e) {
        localStorage.removeItem("todos");
      }
    }
  }
};
</script>
