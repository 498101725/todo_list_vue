<template>
  <div>
    <div>
      <ul class="list">
        <li
          v-for="todoItem in todo"
          :key="todoItem.id"
          v-bind:class="todoStatus(todoItem.complete)"
        >
          <input type="checkbox" v-on:click="toggleTodo(todoItem)" />
          {{ todoItem.name }}
          <button
            class="btn"
            type="button"
            v-on:click="deleteTodo(todoItem.id)"
          >
            X
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DeleteTodo',
  props: {
    todo: {
      type: Array
    }
  },
  methods: {
    toggleTodo: function(todoItem) {
      todoItem.complete = !todoItem.complete;
    },
    deleteTodo: function(id) {
      this.$emit('deleteTodo', id);
    },

    todoStatus: function(status) {
      this.$parent.saveTodos();
      return {
        completed: status == true
      };
    }
  }
};
</script>

<style scoped>
.list {
  list-style: none;
}
.completed {
  text-decoration: line-through;
}
.btn {
  color: red;
  background-color: #e7e7e7;
}
</style>
