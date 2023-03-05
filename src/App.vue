<template>
  <nav class="bg-dark p-3">
    <div class="container nav-items d-flex align-items-center justify-content-between">
      <img src="./assets/logo.svg" alt="" width="36px">
      <ul class="d-flex list-unstyled">
        <li class="nav-item active">
          <a class="nav-link" href="#">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Create</a>
        </li>
      </ul>
    </div>
  </nav>

  <main>
    <div class="container">
      <Alert message="TODO TITLE IS REQUIRED" :show="showalert" type="danger" @close="showalert = false" />

      <section class="form-section">
        <form class="form">
          <div class="form-group">
            <input v-model="todoTitle" type="text" class="form-control" name="" id="" placeholder="ToDo Title">
          </div>
          <button @click.prevent="addTodo" type="submit" class="btn btn-primary">Submit</button>
        </form>
      </section>

      <section class="list">
        <div v-for="todo in todos" class="list-item bg-dark d-flex align-items-center justify-content-between"
          :key="todo.id">
          <h4>{{ todo.title }}</h4>
          <div class="buttons">
            <button @click="removeTodo(todo)" class="btn btn-danger btn-circle">X</button>
          </div>
        </div>
      </section>
    </div>
  </main>
</template>

<script>
import Alert from './components/Alert.vue'

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
    addTodo() {
      if (this.todoTitle === "") {
        this.showalert = true;
        return;
      }
      this.todos.push({
        title: this.todoTitle,
        id: Math.floor(Math.random() * 1000)
      });
    },
    removeTodo(todoTitle) {
      this.todos = this.todos.filter(todo => todo !== todoTitle);
    }
  },
  components: { Alert }
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