<template>
  <div id="app" class="container">
    <h1>MARIShop</h1>
    <product-list :products="products" :maximum="maximum"></product-list>
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";

export default {
  name: "App",
  data: function () {
    return {
      maximum: 50,
      products: [],
    };
  },
  components: {
    ProductList,
  },
  mounted: function () {
    fetch("https://fakestoreapi.com/products")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
};
</script>
