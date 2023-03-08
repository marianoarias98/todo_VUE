<template>
  <NavBar />

  <main>
    <div class="container">
      <Modal title="Edit Todo" :show="editTodoForm.show">
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

      <Alert message="TODO TITLE IS REQUIRED" :show="showalert" type="danger" @close="showalert = false" />

      <section class="form-section">
        <AddTodoForm @submit="addTodo" />
      </section>

      <section class="list">
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

export default {
  data() {
    return {
      todoTitle: "",
      todos: [],
      showalert: false,
      editTodoForm: {
        show: false,
        todo: {
          id: 0,
          title: ""
        }
      }
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
    },

    showEditTodoForm(todo) {
      this.editTodoForm.show = true;
      this.editTodoForm.todo = { ...todo };
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