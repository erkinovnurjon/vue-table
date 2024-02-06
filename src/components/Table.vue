<template>
  <div>
    <table class="custom-table">
      <thead>
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>Status</th>
          <th>Age</th>
          <th>Address</th>
          <th>Role</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(people, index) in paginatedPeople" :key="index">
          <td>{{ people.id }}</td>
          <td>{{ people.name }}</td>
          <td>
            <button
              :class="{
                'active-status': people.status === 'Active',
                'inactive-status': people.status === 'Inactive',
              }"
            >
              {{ people.status }}
            </button>
          </td>
          <td>{{ people.age }}</td>
          <td>{{ people.address }}</td>
          <td>{{ people.role }}</td>
        </tr>
      </tbody>
    </table>
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
  </div>
</template>

<script>
import Button from "./shared/Button.vue";

export default {
  components: {
    Button,
  },
  data() {
    return {
      people: [
        {
          id: 1,
          age: 25,
          name: "John Doe",
          address: "123 Main St",
          status: "Active",
          role: "Admin",
        },
        {
          id: 2,
          age: 30,
          name: "Jane Smith",
          address: "456 Elm St",
          status: "Inactive",
          role: "User",
        },
        {
          id: 3,
          age: 35,
          name: "Bob Johnson",
          address: "789 Oak St",
          status: "Active",
          role: "Admin",
        },
        {
          id: 4,
          age: 28,
          name: "Alice Brown",
          address: "246 Pine St",
          status: "Inactive",
          role: "User",
        },
        {
          id: 5,
          age: 32,
          name: "Michael Wilson",
          address: "135 Cedar St",
          status: "Active",
          role: "Admin",
        },
        {
          id: 6,
          age: 29,
          name: "Emily Jones",
          address: "789 Maple St",
          status: "Inactive",
          role: "User",
        },
        {
          id: 7,
          age: 31,
          name: "David Lee",
          address: "357 Birch St",
          status: "Active",
          role: "Admin",
        },
        {
          id: 8,
          age: 26,
          name: "Sophia Davis",
          address: "951 Willow St",
          status: "Inactive",
          role: "User",
        },
        {
          id: 9,
          age: 33,
          name: "Emma Wilson",
          address: "246 Elm St",
          status: "Active",
          role: "Admin",
        },
        {
          id: 10,
          age: 27,
          name: "James Taylor",
          address: "357 Oak St",
          status: "Inactive",
          role: "User",
        },
        {
          id: 11,
          age: 34,
          name: "Olivia Martinez",
          address: "579 Cedar St",
          status: "Active",
          role: "Admin",
        },
        {
          id: 12,
          age: 24,
          name: "Daniel Harris",
          address: "951 Maple St",
          status: "Inactive",
          role: "User",
        },
        {
          id: 13,
          age: 36,
          name: "Liam Rodriguez",
          address: "357 Pine St",
          status: "Active",
          role: "Admin",
        },
        {
          id: 14,
          age: 23,
          name: "Ava Miller",
          address: "789 Birch St",
          status: "Inactive",
          role: "User",
        },
        {
          id: 15,
          age: 37,
          name: "Mia Brown",
          address: "246 Willow St",
          status: "Active",
          role: "Admin",
        },
        {
          id: 16,
          age: 22,
          name: "Noah Jackson",
          address: "357 Maple St",
          status: "Inactive",
          role: "User",
        },
        {
          id: 17,
          age: 38,
          name: "Ethan White",
          address: "579 Oak St",
          status: "Active",
          role: "Admin",
        },
        {
          id: 18,
          age: 21,
          name: "Isabella Harris",
          address: "951 Cedar St",
          status: "Inactive",
          role: "User",
        },
        {
          id: 19,
          age: 39,
          name: "Aiden Martinez",
          address: "357 Elm St",
          status: "Active",
          role: "Admin",
        },
        {
          id: 20,
          age: 20,
          name: "Sophie Taylor",
          address: "789 Pine St",
          status: "Inactive",
          role: "User",
        },
      ],
      currentPage: 1,
      pageSize: 5,
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.people.length / this.pageSize);
    },
    paginatedPeople() {
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = startIndex + this.pageSize;
      return this.people.slice(startIndex, endIndex);
    },
  },
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
