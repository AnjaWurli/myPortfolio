<template>
  <form>
    <input
      type="text"
      class="todo-style_user-input"
      placeholder="Get sh*t done!"
      v-model="newTodo"
    />
    <button @click.prevent="addTodo" class="todo-style_button">Add</button>
  </form>
  <span v-if="error === 'tooShort'" class="todo-style_error-message"
    >Your input is too short. Use at least 5 characters</span
  >
  <span v-else-if="error === 'double'" class="todo-style_error-message"
    >This To-Do is already there</span
  >
</template>

<script>
export default {
  name: "NewEntryForm",
  emits: ["newEntry"],
  props: {
    todos: Object,
  },
  data() {
    return {
      error: "",
      newTodo: "",
    };
  },
  methods: {
    addTodo() {
      this.error = "";

      this.todos.forEach((todo) => {
        if (this.newTodo === todo.description) {
          this.error = "double";
        }
      });
      if (this.newTodo.length >= 5 && this.error !== "double") {
        const newEntry = {
          description: this.newTodo,
          done: false,
          id: +new Date(),
        };

        /* const response = await fetch("http://localhost:4730/todos", {
          method: "POST",
          headers: { "content-type": "application/json" },
          body: JSON.stringify(newEntry),
        });
        const data = await response.json();*/

        this.newTodo = "";

        this.$emit("newEntry", newEntry);
      } else if (this.newTodo.length < 5) {
        this.error = "tooShort";
      }
    },
  },
};
</script>
