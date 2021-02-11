<template>
  <div id="app" class="container p-4">
    <div class="card shadow p-3 mb-5 bg-white rounded border-0">
      <h1 class="text-center mt-4 fw-bold">Tabel Data</h1>
      <data-form @add:table="addTable" class="mt-4" />
      <know-table
        :tables="tables"
        class="mt-5"
        @delete:table="deleteTable"
        @edit:table="editTable"
      />
    </div>
  </div>
</template>

<script>
import KnowTable from "./components/KnowTable";
import DataForm from "./components/DataForm";
import "../node_modules/bootstrap/dist/css/bootstrap.min.css";
import "@fortawesome/fontawesome-free/css/all.css";
import "@fortawesome/fontawesome-free/js/all.js";

export default {
  name: "app",
  components: {
    KnowTable,
    DataForm,
  },
  data() {
    return {
      tables: [],
    };
  },
   mounted() {
     this.getTables();
   },
  methods: {
     async getTables() {
       try {
         const response = await fetch(
           "https://jsonplaceholder.typicode.com/users"
         );
         const data = await response.json();
         this.tables = data;
       } catch (error) {
         console.error(error);
      }
     },

    async addTable(table) {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users",
          {
            method: "POST",
            body: JSON.stringify(table),
            headers: { "Content-type": "application/json; charset=UTF-8" },
          }
        );
        const data = await response.json();
        this.tables = [...this.tables, data];
      } catch (error) {
        console.error(error);
      }
    },

    async deleteTable(id) {
      try {
        await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
          method: "DELETE",
        });
        this.tables = this.tables.filter((table) => table.id !== id);
      } catch (error) {
        console.error(error);
      }
    },

    async editTable(id, updateTable) {
      try {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/users/${id}`,
          {
            method: "PUT",
            body: JSON.stringify(updateTable),
            headers: { "Content-type": "application/json; charset=UTF-8" },
          }
        );
        const data = await response.json();
        this.tables = this.tables.map((table) =>
          table.id === id ? data : table
        );
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins&display=swap");
body {
  font-family: "Poppins", sans-serif;
}
</style>
