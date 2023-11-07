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
          id: 4,
          name: "Pakora",
          description: "Description for Product 3",
          price: 5,
          imageUrl: "pakora.jpg",
        },
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
