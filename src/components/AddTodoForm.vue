<template>
  <form class="form">
    <div class="form-group">
      <input v-model="todoTitle" type="text" class="form-control" placeholder="ToDo Title">
    </div>
    <Btn @click="$emit('submit', todoTitle)" type="success"  >Submit</Btn>
  </form>
</template>

<script>
import Btn from './Btn.vue';

  export default {
    data() {
        return {
            todoTitle: "",
        };
    },
    emits: ["submit"],
    components: { Btn }
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