<template>
  <select class="select" v-model="pageSize" @change="changePageSize">
    <option value="5">5</option>
    <option value="10">10</option>
    <option value="15">15</option>
    <option value="20">20</option>
  </select>
</template>

<script>
export default {
  data() {
    return {
      pageSize: 5,
    };
  },
  methods: {
    changePageSize(event) {
      const value = event.target.value;
      this.pageSize = parseInt(value);
      this.$emit("change", this.pageSize);
    },
  },
};
</script>
<style>
.select {
  padding: 10px 20px;
  background-color: #ddd;
  border: none;
  outline: none;
}
</style>
