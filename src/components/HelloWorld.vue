<template>
  <div class="hello">
    {{ msg }}
    <form>
      <button @click="addTodo">Add Task</button>
      <button @click="removeTodo">Delete Task</button>
      <p>
        input:
        <input type="text" v-model="newTodo" />
      </p>
      <p>task:{{ newTodo }}</p>
    </form>
    <div>
      <p v-for="todo in todos">
        <input type="checkbox" v-model="todo.done" />
        <input type="checkbox" v-model="todo.editing" />
        <input v-if="todo.editing" v-model="todo.text" @keyup.enter="todo.editing = !todo.editing" />
        <span v-else>{{ todo.text }}</span>
        <button>EDIT</button>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      todos: [
        { text: "vue-router", done: false, editing: false},
        { text: "vuex", done: false, editing: false},
        { text: "vuetify", done: false, editing: false},
        { text: "vue-loader", done: false, editing: false}
      ],
      newTodo: ""
    };
  },
  methods: {
    addTodo: function(event) {
      let text = this.newTodo && this.newTodo.trim();
      if (!text) {
        return;
      }
      this.todos.push({
        text: text,
        done: false
      });
      this.newTodo = "";
    },
    removeTodo: function(event) {
      for (let i = this.todos.length - 1; i >= 0; i--) {
        if (this.todos[i].done) this.todos.splice(i, 1)
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
