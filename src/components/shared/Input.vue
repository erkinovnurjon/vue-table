<template>
  <input
    type="text"
    class="form-control"
    :value="modelValue"
    @input="updateInput"
  />
  <button @click="sortBy">sort</button>
</template>

<script>
export default {
  methods: {
    updateInput(e) {
      this.$emit("update:modelValue", e.target.value);
    },
    sortBy() {
      this.items.sort((a, b) => {
        if (a.name < b.name) {
          return -1;
        }
        if (a.name > b.name) {
          return 1;
        }
        return 0;
      });
    },
  },
  props: {
    modelValue: [String, Number],
  },
};
</script>
<style scoped>
.form-control {
  outline: none;
}
</style>
