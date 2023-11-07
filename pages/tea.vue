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
      ],
    };
  },
};
</script>
