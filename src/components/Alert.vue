<template>
  <div v-if="show" class="alert mt-2 d-flex justify-content-between" :style="{ backgroundColor }">
    <p class="alertTitle">{{ message }}</p>
    <Btn @click="closeAlert" type="danger">X</Btn>
  </div>
</template>

<script>
import Btn from './Btn.vue';

export default {
    props: {
        message: {
            required: true,
            type: String,
        },
        show: {
            required: true,
            type: Boolean,
        },
        type: {
            required: false,
            default: "danger",
            validator(value) {
                return ["danger", "warning", "info"].includes(value);
            }
        }
    },
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
    emits: ["close"],
    methods: {
        closeAlert() {
            this.$emit("close");
        }
    },
    components: { Btn }
}
</script>

<style scoped>
  .alertTitle{
    font-weight: bold;
    margin-bottom: none;
  }
</style>