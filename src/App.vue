<template>
  <NavBar />

  <main>
    <div class="container">
      <Modal title="Edit Todo" :show="editTodoForm.show" @close="editTodoForm.show = false">
        <template #header>
          <h5>Edit Todo</h5>
          <Btn type="secondary" @click="editTodoForm.show = false">X</Btn>
        </template>

        <template #body>
          <form>
            <div class="form-group">
              <label class="mb-2">Todo Title</label>
              <input type="text" class="form-control" placeholder="Enter title" v-model="editTodoForm.todo.title">
            </div>
          </form>
        </template>

        <template #footer>
          <Btn type="success" @click="updateTodo">Submit</Btn>
          <Btn type="secondary" @click="editTodoForm.show = false">Close</Btn>
        </template>
      </Modal>

      <Alert :message="alert.message" :show="alert.show" :type="alert.type" @close="alert.show = false" />

      <section class="form-section">
        <AddTodoForm :isLoading="isPostingTodo" @submit="addTodo" />
      </section>

      <section class="list">
        <Spinner class="spinner" v-if="isLoading" />
        <TodoList v-for="todo in todos" :key="todo.id" :title="todo.title" @remove="removeTodo(todo.id)"
          @edit="showEditTodoForm(todo)" />
      </section>
    </div>
  </main>
</template>

<script>
import AddTodoForm from './components/AddTodoForm.vue';
import Alert from './components/Alert.vue'
import Modal from './components/Modal.vue';
import NavBar from './components/NavBar.vue';
import TodoList from './components/TodoList.vue';
import Btn from './components/Btn.vue';
import axios from "axios";
import Spinner from "./components/Spinner.vue";

export default {
  data() {
    return {
      todoTitle: "",
      todos: [],
      alert: {
        show: false,
        message: "",
        type: "danger"
      },
      editTodoForm: {
        show: false,
        todo: {
          id: 0,
          title: ""
        }
      },
      isLoading: false,
      isPostingTodo: false,
    };
  },
  created() {
    this.fetchTodos();
  },
  methods: {
    async fetchTodos() {
      this.isLoading = true;
      try {
        const res = await axios.get("http://localhost:8080/todos");
        this.todos = await res.data;
      } catch (e) {
        this.showAlert("Failed loading todos");
      }
      this.isLoading = false;
    },

    showAlert(message, type = "danger") {
      this.alert.show = true;
      this.alert.message = message;
      this.alert.type = type;
    },

    async addTodo(title) {
      if (title === "") {
        this.showAlert("Todo title is required");
        return;
      }
      this.isPostingTodo = true;
      const res = await axios.post("http://localhost:8080/todos", {
        title,
      });

      this.isPostingTodo = false;

      this.todos.push(res.data);
    },
    async removeTodo(id) {
      await axios.delete(`http://localhost:8080/todos/${id}`);
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },

    showEditTodoForm(todo) {
      this.editTodoForm.show = true;
      this.fetchTodos()
    },

    updateTodo() {
      const todo = this.todos.find(todo => todo.id === this.editTodoForm.todo.id);
      todo.title = this.editTodoForm.todo.title;
      this.editTodoForm.show = false;
    }
  },
  components: { Alert, AddTodoForm, NavBar, TodoList, Modal, Btn }
}
</script>

<style scoped>

.spinner {
  margin: auto;
  margin-top: 30px;
}
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