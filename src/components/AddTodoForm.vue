<template>
  <form class="form">
    <div class="form-group">
      <input v-model="todoTitle" type="text" class="form-control" placeholder="ToDo Title">
    </div>
    <Btn :disabled="isLoading" type="submit" class="btn btn-primary" @click="$emit('submit', todoTitle)">
      <Spinner v-if="isLoading" />
      <span v-else>Add Todo</span>
    </Btn>
  </form>
</template>

<script>
import Btn from './Btn.vue';
import Spinner from "./Spinner.vue";

export default {
  data() {
    return {
      todoTitle: "",
    };
  },
  emits: ["submit"],
  components: { Btn, Spinner },
  props: {
    isLoading: {
      default: false,
      type: Boolean
    },
  },
};
</script>

<style scoped>
.form {
  display: grid;
  grid-template-columns: 78% 20%;
  gap: 10px;
  margin: auto;
}
</style>