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
          id: 1,
          name: "Kadak Tea",
          description: "Description for Product 1",
          price: 1,
          imageUrl: "tea.jpeg",
        },
        {
          id: 2,
          name: "Milk Tea",
          description: "Description for Product 2",
          price: 2,
          imageUrl: "milk-tea.jpg",
        },
        {
          id: 3,
          name: "Fries",
          description: "Description for Product 3",
          price: 5,
          imageUrl: "fries2.jpeg",
        },
        {
          id: 4,
          name: "Pakora",
          description: "Description for Product 3",
          price: 5,
          imageUrl: "pakora.jpg",
        },
        {
          id: 5,
          name: "Chicken Samosa",
          description: "Description for Product 3",
          price: 5,
          imageUrl: "chicken-samosa.jpg",
        },
        {
          id: 6,
          name: "Alu Samosa",
          description: "Description for Product 3",
          price: 5,
          imageUrl: "alu-samosa.jpg",
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