<template>
  <body class="todo-style_body">
    <header class="todo-style_header">
      <h1 class="todo-style_h1">Todo App</h1>
    </header>
    <main class="todo-style_main">
      <new-entry-form :todos="todos" @newEntry="handleNew" />
      <section class="todo-style_section">
        <filter-options @filterElements="handleFilter" />
        <remove-btn :todos="todos" @remove="handleRemove" />
      </section>
      <todo-list :todos="filtered" />
    </main>
  </body>
</template>

<script>
import FilterOptions from "../components/todoApp/FilterOptions.vue";
import NewEntryForm from "../components/todoApp/NewEntryForm.vue";
import RemoveBtn from "../components/todoApp/RemoveBtn.vue";
import TodoList from "../components/todoApp/TodoList.vue";

export default {
  name: "App",
  components: {
    FilterOptions,
    NewEntryForm,
    RemoveBtn,
    TodoList,
  },
  data() {
    return {
      todos: [
        { id: 1, description: "Learn Vue", done: false },
        { id: 2, description: "Dont get confused", done: true },
      ],
      filtered: [],
    };
  },
  methods: {
    handleFilter(currentFilter) {
      this.filtered = this.todos.filter((todo) => {
        if (currentFilter === "Done") {
          return todo.done === true;
        } else if (currentFilter === "Open") {
          return todo.done === false;
        } else {
          return true;
        }
      });
    },
    handleNew(newEntry) {
      this.todos.push(newEntry);
      this.handleFilter();
    },
    handleRemove(doneTodos) {
      doneTodos.forEach((i) => {
        this.todos.splice(i, 1);
      });
      this.handleFilter();
    },
  },
  created() {
    this.handleFilter();
  },
};
</script>
<!--
    watch this.todos??
  -->
<style>
/*General Styling*/
.todo-style_body {
  font-family: sans-serif;
  font-size: 1.25rem;

  --background: #f5f5f5;
  --color: #ffffff;
  --pink: #ef476f;
  --yellow: #f5ab00;
  --blue: #118ab2;
  --green: #06d6a0;
  --darkblue: #073b4c;

  margin: 0;
  _background-color: var(--background);
}

.todo-style_header {
  background-color: var(--pink);
  padding: 1.65rem;
}

.todo-style_main {
  display: grid;
  justify-content: center;
  position: relative;
}
.todo-style_h1 {
  text-align: center;
  color: var(--color);
  text-shadow: 2px 2px var(--blue);
  filter: drop-shadow(2px 2px var(--yellow));
}

/*Input + Buttons*/
.todo-style_user-input,
.todo-style_button {
  margin-top: 2rem;
  font-size: 1rem;
  border: none;
  padding: 0.6rem;
  border-radius: 7px;
}
.todo-style_button {
  background-color: var(--blue);
  color: var(--color);
  box-shadow: 3px 3px var(--pink);
  margin-left: 0.7rem;
}
.todo-style_button:active {
  outline: 2px solid var(--yellow);
  box-shadow: none;
}
.todo-style_button:focus,
.todo-style_user-input:focus,
.filter:focus {
  outline: 2px solid var(--yellow);
}
.todo-style_user-input {
  width: 12.5rem;
}
.todo-style_error-message {
  color: red;
  font-style: italic;
  position: absolute;
  top: 15%;
  left: 30%;
}
.todo-style_button-remove {
  padding: 0.4rem;
  margin: 0;
}
/*Sections*/
.todo-style_section {
  margin-top: 1.7rem;
}
.todo-style_heading-filter {
  margin-bottom: -0.5rem;
}

/*Filter Options*/
.todo-style_radio-filter {
  all: unset;
  display: inline-block;
  background-color: white;
  outline: 2px solid var(--darkblue);
  width: 20px;
  height: 20px;
  border-radius: 100%;
  translate: 0 60%;
  margin-bottom: 0.5rem;
}
.todo-style_radio-filter:checked {
  background-color: var(--blue);
}
.todo-style_li {
  all: unset;
  display: block;
  margin-left: -2rem;
}

/* ToDos*/
.todo-style_li-todo {
  background-color: white;
  color: black;
  padding: 0.5rem;
  width: 16rem;
  border-radius: 7px;
  margin-block: 0.5rem;
}
.todo-style_li-todo:focus-within {
  box-shadow: 5px 5px var(--pink);
  outline: 0.1rem solid var(--yellow);
}
.todo-style_checkbox-todo {
  all: unset;
  display: inline-block;
  width: 15px;
  height: 15px;
  background-color: white;
  border: 2px solid var(--darkblue);
  border-radius: 3px;
  margin-inline: 0.5rem;
  translate: 0 10%;
  position: relative;
}

.todo-style_checkbox-todo:after {
  content: "";
  display: block;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 2px 2px 0;
  rotate: 45deg;
  position: relative;
  top: -40%;
  left: 50%;
  translate: -50% 50%;
}
.todo-style_checkbox-todo:checked {
  background-color: var(--green);
}
.todo-style_checkbox-todo:checked + label {
  text-decoration: line-through;
}
.todo-style_label {
  display: inline-block;
  width: 80%;
  padding-left: 0.25rem;
}
</style>
<!--
  Todo:
  -"Done" is still clicked when new entry added
  -toggle "remove" button when no todo is done
  -watcher for render filtered todos?
-->
