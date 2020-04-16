<template>
  <div>
    <input placeholder="enter todo here..." v-model="message" />

    <button v-on:click="addTodo(message)">add another todo</button>
  </div>
</template>

<script>
import { v4 } from 'uuid';

export default {
  name: 'AddTodo',
  data: function() {
    return {
      message: ''
    };
  },

  methods: {
    addTodo(message) {
      const newTodo = {
        id: v4(),
        name: message,
        complete: false
      };

      this.$emit('addTodo', newTodo);
      this.message = '';
    }
  }
};
</script>

<style scoped></style>
