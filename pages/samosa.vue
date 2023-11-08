<template>
  <div>
    <v-container>
      <ProductCard :products="products" />
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
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
    };
  },
  methods: {
    order(product) {
      console.log(product);
      // Implement your cart functionality here
      // You can use Vuex or another state management solution for this.
    },
  },
};
</script>