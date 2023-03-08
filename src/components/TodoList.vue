<template>
  <div class="list-item bg-dark d-flex align-items-center justify-content-between">
    <h4>{{ title }}</h4>
    <div class="buttons">
      <Btn type="warning" @click="$emit('edit')">E</Btn>
      <Btn @click="$emit('remove')" type="danger">X</Btn>
    </div>
  </div>
</template>

<script>
import Btn from './Btn.vue';
export default {
  props: {
    title: {
      required: true,
      type: String,
    },
  },
  emits: ['remove', 'edit'],
  components: { Btn }
};
</script>


<style scoped>
.list-item {
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 10px;
}

.buttons{
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 6px;
}
</style>