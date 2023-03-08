<template>
  <div v-if="show" class="modal">
    <div class="modal-dialog">
      <div class="modal-content">

        <div class="modal-header bg-dark">
          <slot name="header" />
        </div>

        <div class="modal-body bg-dark">
          <slot name="body" />
        </div>

        <div class="modal-footer bg-dark">
          <slot name="footer" />
        </div>
      </div>
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
    show: {
      default: false
    }
  },
  components: { Btn },
  computed: {
    backgroundColor() {
      const options = {
        danger: "var(--danger-color)",
        info: "var(--info-color)",
        warning: "var(--warning-color)",
      };
      return options[this.type];
    }
  },
  methods: {
    close: {
      show: false
    }
  }
}
</script>

<style scoped>
.modal {
  color: #ffffff;
  display: block;
}

.modal-header {
  border: none;
}

span {
  color: white;
}

.modal-body{
  padding: 30px 15px;
}
</style>