<template>
  <div>
    <v-container>
      <v-alert v-if="response" color="primary" dark>
        {{ response.message }}
      </v-alert>

      <div class="text-center">
        <v-dialog v-model="dialog" width="500">
          <v-card>
            <v-card-title class="text-h5"> Product Category </v-card-title>

            <v-card-text class="my-5">
              <v-text-field
                v-model="payload.name"
                outlined
                dense
                label="Name"
                required
              ></v-text-field>
              <v-text-field
                v-model="payload.description"
                outlined
                dense
                label="Description"
              ></v-text-field>
            </v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn small @click="dialog = false" color="grey">Close</v-btn>
              <v-btn v-if="isNew" small @click="submit" color="primary"
                >Submit</v-btn
              >
              <v-btn v-else small @click="update" color="primary">Update</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>

      <v-card elevation="5">
        <v-data-table
          :headers="headers"
          :items="productCategories.data"
          :options.sync="options"
          :server-items-length="productCategories.total"
          :loading="loading"
          class="elevation-1"
        >
          <template v-slot:top>
            <v-toolbar flat>
              <v-toolbar-title>Product Categories</v-toolbar-title>
              <v-spacer></v-spacer>
              <v-icon color="primary" @click="(dialog = true), (isNew = true)"
                >mdi-plus-circle-outline</v-icon
              >
            </v-toolbar>
          </template>
          <template v-slot:item.actions="{ item }">
            <v-icon @click="editProductCategory(item)" class="mr-2"
              >mdi-pencil</v-icon
            >
            <v-icon @click="deleteProductCategory(item.id)" color="red"
              >mdi-delete</v-icon
            >
          </template>
        </v-data-table>
      </v-card>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      response: null,
      loading: true,
      options: {},
      payload: {
        name: "",
        description: "",
      },
      productCategories: [],
      headers: [
        { text: "ID", value: "id" },
        { text: "Name", value: "name" },
        { text: "Actions", value: "actions", sortable: false },
      ],
      isNew: false,
    };
  },
  created() {
    this.loadProductCategories();
  },
  watch: {
    options: {
      handler() {
        this.loadProductCategories();
      },
      deep: true,
    },
  },
  methods: {
    loadProductCategories() {
      this.$axios
        .get("http://127.0.0.1:8000/api/product-categories", {
          params: { ...this.options },
        })
        .then(({ data }) => {
          this.productCategories = data;
          this.loading = false;
        })
        .catch((error) => {
          console.error("Error fetching product categories:", error);
        });
    },
    submit() {
      this.$axios
        .post(`http://127.0.0.1:8000/api/product-categories`, this.payload)
        .then(({ data, status }) => {
          this.response = {
            message:
              status == 201 ? "Product Category Interted" : "Error Occurred",
          };

          this.loadProductCategories();

          setTimeout(() => (this.response = null,this.dialog = false), 3000);
        });
      // Implement your cart functionality here
      // You can use Vuex or another state management solution for this.
    },
    update() {
      this.$axios
        .put(`http://127.0.0.1:8000/api/product-categories/${this.payload.id}`, this.payload)
        .then(({ status }) => {
          this.response = {
            message:
              status == 200 ? "Product Category updated" : "Error occured",
          };

          this.loadProductCategories();

          setTimeout(() => (this.response = null,this.dialog = false), 3000);
        });
    },
    editProductCategory(item) {
      this.isNew = false;
      this.dialog = true;
      this.payload = item;
    },
    deleteProductCategory(id) {
      this.$axios
        .delete(`http://127.0.0.1:8000/api/product-categories/${id}`)
        .then(({ status }) => {
          this.response = {
            message:
              status == 204 ? "Product Category deleted" : "Error Occurred",
          };

          this.loadProductCategories();

          setTimeout(() => (this.response = null,this.dialog = false), 3000);
        });
    },
  },
};
</script>
