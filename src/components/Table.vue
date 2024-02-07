<template>
  <div>
    <b-icon icon="arrow-up"></b-icon>
    <table class="custom-table">
      <thead>
        <tr>
          <th v-for="(field, index) in fields" :key="index">{{ field }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in paginatedPeople" :key="index">
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
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
          <td>{{ item.role }}</td>
        </tr>
      </tbody>
    </table>
    <div>
      <select class="select" v-model="pageSize" @change="changePageSize">
        <option value="5">5</option>
        <option value="10">10</option>
        <option value="15">15</option>
        <option value="20">20</option>
      </select>
      <div class="page-buttons">
        <div class="pagination">
          <button
            class="page-button"
            @click="prevPage"
            :disabled="currentPage === 1"
            :page="currentPage"
          >
            prev
          </button>
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
          <button
            class="page-button"
            @click="nextPage"
            :disabled="currentPage === totalPages"
          >
            Next
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Button from "./shared/Button.vue";
import Select from "./shared/Select.vue";

export default {
  components: {
    Button,
    Select,
  },
  props: {
    fields: {
      type: Array,
      required: true,
    },
    items: {
      type: Array,
      required: true,
    },
    fields1: {
      type: Array,
      required: true,
    },
    items2: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      currentPage: 1,
      pageSize: 5,
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.items.length / this.pageSize);
    },
    paginatedPeople() {
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = startIndex + this.pageSize;
      return this.items.slice(startIndex, endIndex);
    },
  },
  methods: {
    changePage(page) {
      this.currentPage = page;
    },
    changePageSize(event) {
      const value = event.target.value;
      this.pageSize = parseInt(value);
      this.$emit("change", this.pageSize);
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
.custom-table {
  width: 100%;
  border-collapse: collapse;
}

.custom-table th,
.custom-table td {
  border: 1px solid #ddd;
  padding: 8px;
}

.custom-table th {
  background-color: #f2f2f2;
  text-align: left;
}

.active-status {
  width: 100px;
  height: 30px;
  border-radius: 9px;
  border: none;
  background-color: rgb(71, 157, 71);
  color: white;
}

.inactive-status {
  width: 100px;
  height: 30px;
  border-radius: 9px;
  border: none;
  background-color: rgb(160, 46, 46);
  color: white;
}

.active-status:hover,
.inactive-status:hover {
  opacity: 0.7;
}
td:hover {
  background-color: #ddd;
}
td:active {
  border-color: #f2f2f2;
}
.page-buttons {
  display: flex;
  justify-content: center;
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
