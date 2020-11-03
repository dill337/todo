<template>
  <div class="mainDiv">
    <div>
      <h1 class="title1">To Do List</h1>
    </div>
    <md-field class="inputfield">
      <md-input
        class="inputText"
        v-model="currentTodo"
        @keydown.enter="addTodo()"
        placeholder="Add a todo"
      >
      </md-input>
    </md-field>
    <ul class="todos">
      <li
        v-for="todo in todos"
        :key="todo.id"
        :class="{ editing: todo == editedTodo }"
      >
        <!-- {{ todo.label }} -->
        <p
          class="title"
          contenteditable="true"
          v-on:keydown.enter="editedTodo($event, todo)"
          v-on:blur="editedTodo($event, todo)"
          v-bind:class="{ completed: todo.completed }"
        >
          {{ todo.label }}
        </p>
        <input
          type="checkbox"
          v-on:change="completedTodo(todo)"
          v-bind:checked="todo.completed"
        />
        <button class="deletebutton" @click="removeTodo(todo)">
          Delete Task
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        editedToDoId: false,
        completed: false,
      });
      this.currentTodo = "";
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    completedTodo(todo) {
      todo.completed = !todo.completed;
    },
    editToDo(todo) {
      return "<input>" + todo.label + "</input>";
      // todo.editedToDoId = true;
      // placeholder=todo.label
    },
  },
};
</script>

<style>
.title1 {
  color: red;
  padding: 50px;
  margin: auto;
  text-align: center;
}
.mainDiv {
  background-color: black;
}
.inputfield {
  left: 50px;
}
.inputText {
  color: gray;
}
.completed {
  text-decoration: line-through;
}
.not-completed {
  color: black;
}
.deletebutton {
  border: none;
  color: orange;
  background-color: black;
  position: relative;
  left: 100px;
  cursor: pointer;
}
.editing {
  display: block;
}
.todos {
  color: blue;
  list-style-type: none;
}
div {
  background-color: black;
  position: center;
}
body {
  background-color: black;
}
</style>
