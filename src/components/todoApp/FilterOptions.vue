<template>
  <h2 class="todo-style_heading-filter">Filter & Options</h2>
  <ul>
    <li
      v-for="filter of filterOptions"
      @click="filterElements(filter)"
      :key="filter.name"
      class="todo-style_li"
    >
      <input
        type="radio"
        class="todo-style_radio-filter"
        :id="filter.name"
        name="filter"
        :checked="filter.checked"
      />
      <label :for="filter.name" class="todo-style_label">
        {{ filter.name }}
      </label>
    </li>
  </ul>
</template>

<script>
export default {
  name: "FilterOptions",
  emits: ["filterElements"],
  data() {
    return {
      filterOptions: [
        { name: "All", checked: true },
        { name: "Open", checked: false },
        { name: "Done", checked: false },
      ],
      currentFilter: "",
    };
  },
  methods: {
    filterElements(filter) {
      this.currentFilter = filter.name;
      return this.$emit("filterElements", this.currentFilter);
    },
  },
};
</script>
