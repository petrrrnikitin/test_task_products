<template>
  <div id="app">
    <main class="grid container">
      <div class="sub_category_page">
        <div
          v-if="!loading"
          class="column_right column_right_products_container"
        >
          <div class="product__area">
            <div id="products_section">
              <div class="products_page pg_0">
                <Product
                  :key="product.id"
                  v-for="product in products"
                  :product="product"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";
import Product from "./components/Product";

export default {
  name: "App",
  components: { Product },
  data() {
    return {
      products: {},
      loading: true
    };
  },
  created() {
    axios.get("products.json").then(response => {
      this.products = response.data;
      this.loading = false;
    });
  }
};
</script>
<style>
.column_right {
  width: 100%;
}
.sub_category_page .column_right_products_container {
  width: 100%;
}
</style>
