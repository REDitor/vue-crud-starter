<template>
  <section>
    <div class="container">
      <h2 class="mt-3 mt-lg-5">Products</h2>
        <button type="button" class="btn btn-primary mt-3" @click="this.$router.push('/createproduct');">
            Add product
          </button>
      <div class="row mt-3">
        <product-list-item
          v-for="product in products"
          :key="product.id"
          :product="product"
          @updateProducts="updateProducts"
        />
      </div>
    </div>
  </section>
</template>

<script>
import ProductListItem from "./ProductListItem.vue";
import axios from 'axios';

export default {
  name: "ProductList",
  components: {
    ProductListItem,
  },
  data() {
    return {
      products: [],
    };
  },
  mounted() {
    this.updateProducts();
  },
  methods: {
    updateProducts() {
      axios
        .get('http://localhost/products')
        .then(res => {
          this.products = res.data;
        })
        .catch((err) => console.error(err));
    }
  }
};
</script>

<style>
</style>