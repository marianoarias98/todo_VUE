<template>
  <div class="list-item bg-dark d-flex align-items-center justify-content-between">
    <h4>{{ title }}</h4>
    <div class="buttons">
      <button @click="$emit('remove')" class="btn btn-danger btn-circle">X</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      required: true,
      type: String,
    },
  },
  emits: ['remove']
};
</script>


<style scoped>
.list-item {
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 10px;
}
</style>