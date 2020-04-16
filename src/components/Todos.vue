<template>
  <div>
    <AddTodo v-on:addTodo="addItem" />
    <DeleteTodo v-bind:todo="todos" v-on:deleteTodo="deleteItem" />
  </div>
</template>

<script>
import DeleteTodo from './DeleteTodo.vue';
import AddTodo from './AddTodo.vue';

export default {
  name: 'Todos',
  components: {
    DeleteTodo,
    AddTodo
  },
  data: function() {
    return {
      todos: [
        // { id: 0, name: 'ManUnderRain React', complete: true },
        // { id: 1, name: 'Menu Redux', complete: false },
        // { id: 2, name: 'Vue Learning', complete: false }
      ]
    };
  },
  //mounted 方法现在需要先获取数据，然后对 JSON 格式的数据进行解析。如果这里出现了任何错误，我们就认为数据已经损坏了并将它删除
  mounted() {
    if (localStorage.getItem('todos')) {
      try {
        this.todos = JSON.parse(localStorage.getItem('todos'));
      } catch (e) {
        localStorage.removeItem('todos');
      }
    }
  },

  methods: {
    addItem(newTodo) {
      if (!this.todos) {
        return;
      }
      this.todos.push(newTodo);
      this.saveTodos();
    },

    deleteItem(id) {
      const index = this.todos.findIndex(todo => {
        return todo.id === id;
      });
      this.todos.splice(index, 1);
      this.saveTodos();
    },
    saveTodos() {
      // 转成JSON字符串；
      const parsed = JSON.stringify(this.todos);
      // 存储数据;
      localStorage.setItem('todos', parsed);
    }
  }
};
</script>

<style scoped></style>
