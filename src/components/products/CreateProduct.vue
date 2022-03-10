<template>
  <section>
    <div class="container">
      <form ref="form">
        <h2 class="mt-3 mt-lg-5">Create a product</h2>
        <h5 class="mb-4"></h5>

        <div class="input-group mb-3">
          <span class="input-group-text">Name</span>
          <input type="text" class="form-control" v-model="product.name" />
        </div>

        <div class="input-group mb-3">
          <span class="input-group-text">Price</span>
          <input type="number" class="form-control" v-model="product.price" />
        </div>

        <div class="input-group mb-3">
          <span class="input-group-text">Description</span>
          <textarea
            class="form-control"
            v-model="product.description"
          ></textarea>
        </div>

        <div class="input-group mb-3">
          <span class="input-group-text">Image URL</span>
          <input type="text" class="form-control" v-model="product.image" />
        </div>

        <div class="input-group mb-3">
          <span class="input-group-text">Category</span>
          <select v-model="product.category_id" class="form-select">
            <option v-for="category in categories" :key="category.id" :value="category.id">{{ category.name }}</option>
          </select>
        </div>

        <div class="input-group mt-4">
          <button type="button" class="btn btn-primary" @click="createProduct">Create product</button>
          <button
            type="button"
            class="btn btn-danger"
            @click="this.$router.push('/products')"
          >
            Cancel
          </button>
        </div>
      </form>
    </div>
  </section>
</template>

<script>
import axios from 'axios';
export default {
  name: "CreateProduct",
  data() {
    return {
      product: {
        name: "",
        price: "",
        description: "",
        image: "",
        category_id: 0,
      },
      categories: [],
    };
  },
  mounted() {
    this.getCategories();
  },
  methods: {
    getCategories() {
      axios
        .get('http://localhost/categories')
        .then((res) => {
          this.categories = res.data;
        })
        .catch((err) => console.error(err));
    },
    createProduct() {
      //TODO: product not showing up when reaching page without extra reload
      axios
        .post('http://localhost/products', this.product)
        .then((res) => {
          console.log(res);
          this.$router.push('/products');
        })
        .catch((err) => console.error(err));
    }
  }
};
</script>

<style>
</style>