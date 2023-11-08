<template>
  <v-row>
    <v-col v-for="product in products" :key="product.id" cols="12" md="4">
      <v-card>
        <v-img
          :src="product.image_url"
          class="mx-auto"
          max-height="350"
          max-width="350"
          contain
        ></v-img>
        <v-card-title>{{ product.name }} {{ product.price }} AED</v-card-title>
        <v-card-text>
          <v-btn block color="primary" @click="order(product)">order</v-btn>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  props: ["products"],
  data() {
    return {};
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
