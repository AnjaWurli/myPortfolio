<template>
  <section class="todo-style_section">
    <h2 class="todo-style_heading-filter">Your Todos</h2>
    <ul id="todo-list">
      <li
        v-for="todo of todos"
        class="todo-style_li-todo todo-style_li"
        :key="todo.id"
      >
        <input
          class="todo-style_checkbox-todo"
          type="checkbox"
          v-model="todo.done"
          :id="todo"
        />
        <label :for="todo" class="todo-style_label">{{
          todo.description
        }}</label>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "TodoList",
  props: { todos: Object },
};
</script>
