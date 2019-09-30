<template>
  <div id="app">
    <Navbar />
    <b-container>
      <b-row class="justify-content-center">
        <AddProduct @addProduct="addProduct" />
        <ListProduct
          :products="productList"
          @delProduct="delProduct"
          @updateProduct="updateProduct"
        />
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import AddProduct from "./components/AddProduct.vue";
import ListProduct from "./components/ListProduct.vue";
import axios from "axios";
import UpdateProduct from "./components/UpdateProduct.vue";

export default {
  name: "app",
  components: {
    Navbar,
    ListProduct,
    AddProduct,
    UpdateProduct
  },
  data() {
    return {
      productList: []
    };
  },
  methods: {
    async getProductList() {
      try {
        let result = await axios.get("http://localhost:3000/products");
        console.log("result", result.data);
        this.productList = result.data;
      } catch (error) {
        console.log("Error", error);
      }
    },
    async addProduct(newProduct) {
      console.log("newProduct", newProduct);
      try {
        await axios.post("http://localhost:3000/products", newProduct);
        this.getProductList();
      } catch (error) {
        console.log("Error", error);
      }
    },
    async delProduct(productid) {
      try {
        await axios.delete("http://localhost:3000/products/" + productid);
        this.getProductList();
      } catch (error) {
        console.log("Error", error);
      }
      console.log("productid", productid);
    },
    async updateProduct(updatedProduct) {
      try {
        await axios.put(
          `http://localhost:3000/products/${updatedProduct.id}`,
          updatedProduct
        );
        this.getProductList();
      } catch (error) {
        console.log("Error", error);
      }
    }
  },
  mounted() {
    this.getProductList();
  }
};
</script>

<style lang="scss">
</style>
