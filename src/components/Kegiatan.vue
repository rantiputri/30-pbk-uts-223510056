<template>
  <div>
    <h2>Data Todos</h2>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo.title" placeholder="Title" required>
      <button type="submit">Add Todo</button>
    </form>
    <ul v-if="data.length > 0">
      <li v-for="todo in data" :key="todo.id">
        <input type="checkbox" v-model="todo.completed" disabled>
        <span :class="{ 'completed': todo.completed }">{{ todo.title }}</span>
      </li>
    </ul>
    <p v-else>No data available</p>
  </div>
</template>

<script>
export default {
  name: 'DataKegiatan',
  props: {
    data: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      newTodo: {
        title: '',
        completed: false
      }
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.title.trim() === '') return;
      this.$emit('add-todo', this.newTodo);
      this.newTodo.title = '';
      this.newTodo.completed = false;
    }
  }
}
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>
