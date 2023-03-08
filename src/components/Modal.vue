<template>
  <div ref="modal" v-show="show" class="modal">
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
  data() {
    return {
      clickListener: (e) => {
        console.log(e.target);
        if (e.target === this.$refs.modal) {
          this.$emit("close");
        }
      },
      closeOnEscapeListener: (e) => {
        if (e.key === "Escape") {
          this.$emit('close');
        }
      }
    };
  },
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
  },
  emits: ["close"],
  mounted() {
    window.addEventListener("click", this.clickListener);
    window.addEventListener("keydown", this.closeOnEscapeListener);
  },
  beforeUnmount() {
    window.removeEventListener("click", this.clickListener);
    window.removeEventListener("keydown", this.closeOnEscapeListener);
  },
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