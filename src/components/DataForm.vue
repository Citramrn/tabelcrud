<template>
  <div id="data-form" class="container">
    <form @submit.prevent="buttonSubmit" ref="anyName" @submit="resetForm">
      <input
        class="form-control"
        type="text"
        placeholder="Name"
        v-model="table.name"
      />
      <input
        class="form-control mt-3"
        type="text"
        placeholder="Email"
        ref="first"
        v-model="table.email"
      />
      <input
        class="form-control mt-3"
        type="text"
        ref="first"
        placeholder="Website"
        v-model="table.website"
      />
      <button class="btn btn-dark mt-4 p-2">Add Table</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "data-form",
  data() {
    return {
      error: false,
      succes: false,
      table: {
        name: "",
        email: "",
        website: "",
      },
    };
  },
  methods: {
    buttonSubmit() {
      this.$emit("add:table", this.table);
    },

    resetForm() {
      this.$refs.anyName.reset();
    },
  },
};
</script>

<style>
.site:hover {
  background-color: rgb(94, 94, 94);
}
</style>
