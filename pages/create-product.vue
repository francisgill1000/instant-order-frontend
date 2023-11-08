<template>
  <div>
    <v-container>
      <!-- <ProductCard :products="products" /> -->
      <v-text-field
        v-model="payload.name"
        outlined
        dense
        label="product title"
      />
      <v-text-field
        v-model="payload.price"
        type="number"
        outlined
        dense
        label="product price"
      />
      <!-- 
      <v-file-input
        prepend-icon=""
        v-model="payload.image_url"
        outlined
        dense
        label="Click to upload image"
        accept="image/*"
        @change="handleFileChange"
      ></v-file-input>
 -->
      <v-textarea
        v-model="payload.description"
        outlined
        dense
        label="product image"
      />

      <v-fade-transition transition="scroll-y-transition">
        <v-alert v-if="response" class="info pa-1 my-1">
          {{ response.message }}
        </v-alert>
      </v-fade-transition>

      <!-- {{ imagePreviews }}
      <img :src="imagePreview" v-if="imagePreview" alt="Image Preview" /> -->

      <v-btn @click="submit">Submit</v-btn>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      response: null,
      payload: {
        name: "",
        price: "",
        image_url: "",
        description: "",
      },
      products: [
        {
          id: 5,
          name: "Chicken Samosa",
          description: "Description for Product 3",
          price: 5,
          image_url: "chicken-samosa.jpg",
        },
        {
          id: 6,
          name: "Alu Samosa",
          description: "Description for Product 3",
          price: 5,
          image_url: "alu-samosa.jpg",
        },
        // Add more product data here
      ],
      imagePreview: null,
      selectedImage: null, // Store the selected file separately
    };
  },
  methods: {
    handleFileChange() {
      if (this.payload.image_url) {
        const reader = new FileReader();
        reader.onload = () => {
          this.payload.image_url = reader.result;
          this.imagePreview = reader.result; // Set the preview image source
        };
        reader.readAsDataURL(this.payload.image_url);
      } else {
        // Handle the case where no file is selected or the input is undefined
        // You can display an error message or take other appropriate action here
      }
    },
    submit() {
      this.$axios
        .post(`http://127.0.0.1:8000/api/product`, this.payload)
        .then(({ data, status }) => {
          this.response = {
            message: status == 201 ? "Product Interted" : "Error Occurred",
          };

          setTimeout(() => (this.response = null), 3000);
        });
      // Implement your cart functionality here
      // You can use Vuex or another state management solution for this.
    },
  },
};
</script>
