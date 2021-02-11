<template>
  <div id="know-table" class="container table-responsive">
    <table class="table">
      <thead class="bg-dark text-white">
        <tr>
          <th>No</th>
          <th>Name</th>
          <th>Email</th>
          <th>Website</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr :key="table.id" v-for="(table, index) in tables">
          <td>{{ index + 1 }}</td>
          <td v-if="editting === table.id">
            <input
              class="form-control"
              type="text"
              placeholder="Name"
              ref="first"
              v-model="table.name"
            />
          </td>
          <td v-else>{{ table.name }}</td>
          <td v-if="editting === table.id">
            <input
              class="form-control"
              type="text"
              placeholder="Email"
              ref="first"
              v-model="table.email"
            />
          </td>
          <td v-else>{{ table.email }}</td>
          <td v-if="editting === table.id">
            <input
              class="form-control"
              type="text"
              placeholder="Website"
              v-model="table.website"
            />
          </td>
          <td v-else>{{ table.website }}</td>
          <td v-if="editting === table.id">
            <button class="btn site" @click="editTable(table)">Save</button>
            <button class="btn site" @click="cancelEdit(table)">Cancel</button>
          </td>
          <td v-else>
            <button class="btn site" @click="editButton(table)">Edit</button>
            <button class="btn site" @click="$emit('delete:table', table.id)">
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "know-table",
  props: {
    tables: Array,
  },
  data() {
    return {
      editting: null,
    };
  },
  methods: {
    editTable(table) {
      if (table.name === "" || table.email === "" || table.website === "")
        return;
      this.$emit("edit:table", table.id, table);
      this.editting = null;
    },

    editButton(table) {
      this.cachedTable = Object.assign({}, table);
      this.editting = table.id;
    },
    cancelEdit(table) {
      Object.assign(table, this.cachedTable);
      this.editting = null;
    },
  },
};
</script>

<style>
/* Darker background on mouse-over */
.site:hover {
  background-color: rgb(143, 143, 143);
}
</style>


