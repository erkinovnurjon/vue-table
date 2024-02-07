<template>
  <button class="button" disabled="">
    <slot />
  </button>
</template>
<script>
export default {
  props: {
    currentPage: {
      type: Function,
      required: true,
    },
  },
};
</script>
<style>
.button {
  padding: 10px 18px;
  border-radius: 6px;
  border: none;
  background-color: rgb(187, 154, 76);
  color: black;
  font-weight: 500;
  text-align: center;
}
.button:hover {
  opacity: 0.7;
  transition: all ease 0.5s;
}
</style>

<!-- <td>{{ item.name }}</td>
          <td>
            <button
              :class="{
                'active-status': item.status === 'Active',
                'inactive-status': item.status === 'Inactive',
              }"
            >
              {{ item.status }}
            </button>
          </td>
          <td>{{ item.age }}</td>
          <td>{{ item.address }}</td>
          <td>{{ item.role }}</td> -->
