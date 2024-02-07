<template>
  <div class="page-buttons">
    <button
      class="page-button"
      @click="prevPage"
      :disabled="currentPage === 1"
      :page="currentPage"
    >
      Previous
    </button>
    <div class="pagination">
      <button
        v-for="page in totalPages"
        :key="page"
        @click="changePage(page)"
        :class="{
          'page-button': true,
          'active-page': currentPage === page,
          'other-page': currentPage !== page,
        }"
      >
        {{ page }}
      </button>
    </div>

    <button
      class="page-button"
      @click="nextPage"
      :disabled="currentPage === totalPages"
    >
      Next
    </button>
  </div>
</template>
<script>
export default {
  methods: {
    changePage(page) {
      this.currentPage = page;
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
  },
};
</script>
<style>
.page-buttons {
  display: flex;
  justify-content: space-between;
  width: 100%;
  border: 0.5px solid #ddd;
}
.page-button {
  padding: 8px 15px;
  border-radius: 6px;
  border: none;
  background-color: #beba83;
}
.pagination {
  display: flex;
  justify-content: center;
  gap: 5px;
}
.active-page {
  background-color: #ab9b57;
}
</style>
