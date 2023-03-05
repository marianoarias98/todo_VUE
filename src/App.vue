<template>
 <NavBar/>

  <main>
    <div class="container">
      <Alert message="TODO TITLE IS REQUIRED" :show="showalert" type="danger" @close="showalert = false" />

      <section class="form-section">
        <AddTodoForm @submit="addTodo"/>
      </section>

      <section class="list">
        <TodoList v-for="todo in todos" :key="todo.id" :title="todo.title" @remove="removeTodo(todo.id)"/>
      </section>
    </div>
  </main>
</template>

<script>
import AddTodoForm from './components/AddTodoForm.vue';
import Alert from './components/Alert.vue'
import NavBar from './components/NavBar.vue';
import TodoList from './components/TodoList.vue';

export default {
  components: {
    Alert,
  },
  data() {
    return {
      todoTitle: "",
      todos: [],
      showalert: false,
    };
  },
  methods: {
    addTodo(title) {
      if (title === "") {
        this.showalert = true;
        return;
      }
      this.todos.push({
        title,
        id: Math.floor(Math.random() * 1000)
      });
    },
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    }
  },
  components: { Alert, AddTodoForm, NavBar, TodoList }
}
</script>

<style scoped>
.form {
  display: grid;
  grid-template-columns: 78% 20%;
  gap: 10px;
  margin: auto;
}

.list-item {
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 10px;
}

section {
  padding-top: 30px;
}

li {
  margin-left: 20px;
  margin-bottom: 0;
}
</style>