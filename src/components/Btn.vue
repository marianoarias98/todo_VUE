<template>
  <button @click.prevent="$emit('click')" class="btn" :style="{ backgroundColor }" type="submit">
  <slot />
  </button>
</template>

<script>
export default {
  props: {
    "type": {
      required: true,
      type: String,
      default: "success",
      validator(value) {
        return ["success","danger", "warning", "info"].includes(value);
      }
    }
  },
  computed: {
    backgroundColor() {
      const options = {
        success: "var(--success-color)",
        danger: "var(--danger-color)",
        info: "var(--info-color)",
        warning: "var(--warning-color)",
        secondary: "var(--secondary-color)"
      }
      return options[this.type];
    }
  },
  emits:['click'],
}
</script>

<style scoped>
button{
  color: white;
  font-weight: bold;
  border: 1px solid rgba(0, 0, 0, 0.516);
}
.btn:disabled {
  opacity: 80%;
}
</style>