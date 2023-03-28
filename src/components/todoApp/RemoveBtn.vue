<template>
  <button @click="remove" class="todo-style_button todo-style_button-remove">
    Remove Done Todos
  </button>
</template>

<script>
export default {
  name: "RemoveBtn",
  props: { todos: Object },
  methods: {
    remove() {
      let doneTodos = [];
      for (let i = this.todos.length - 1; i >= 0; i--) {
        if (this.todos[i].done === true) {
          /* await fetch(`http://localhost:4730/todos/${this.todos[i].id}`, {
            method: "DELETE",
          });*/
          doneTodos.push(i);
        }
      }
      return this.$emit("remove", doneTodos);
    },
  },
};
</script>
