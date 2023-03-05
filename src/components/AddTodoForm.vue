<template>
  <form class="form">
    <div class="form-group">
      <input v-model="todoTitle" type="text" class="form-control" placeholder="ToDo Title">
    </div>
    <button @click.prevent="$emit('submit', todoTitle)" type="submit" class="btn btn-primary">Submit</button>
  </form>
</template>

<script>
  export default {
  data() {
    return {
      todoTitle: "",
    };
  },
  emits: ["submit"],
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