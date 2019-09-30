<template>
  <b-col md="4" class="m-3">
    <b-card header="List Product">
      <b-card-group deck>
        <b-card
          :border-variant="product.inventoryStatus? 'success' : 'danger'"
          align="center"
          style="border: 2px solid"
          :key="product.id"
          v-for="product in products"
          class="productCard"
        >
          <b-badge
            class="mb-3"
            :variant="product.inventoryStatus? 'success' : 'danger'"
          >{{ product.inventoryStatus? 'In Stock' : 'On Backorder'}}</b-badge>
          <b-card-text>
            <strong>Name:</strong>
            {{ product.name }}
          </b-card-text>
          <b-card-text>
            <strong>Price:</strong>
            {{ product.price }}
          </b-card-text>
          <b-card-text>
            <strong>Brand:</strong>
            {{ product.brand }}
          </b-card-text>
          <hr class="p-2" />
          <b-row>
            <b-col>
              <b-button variant="danger" @click="delProduct(product.id)">
                <i class="far fa-trash-alt"></i>
              </b-button>
            </b-col>
            <b-col>
              <UpdateProduct :product="product" @updateProduct="updateProduct" />
            </b-col>
          </b-row>
        </b-card>
      </b-card-group>
    </b-card>
  </b-col>
</template>
<script>
import UpdateProduct from "./UpdateProduct.vue";
export default {
  name: "ListProduct",
  props: ["products"],
  components: {
    UpdateProduct
  },
  methods: {
    delProduct(productid) {
      this.$emit("delProduct", productid);
    },
    updateProduct(updatedProduct) {
      this.$emit("updateProduct", updatedProduct);
    }
  }
};
</script>
<style scoped lang="scss">
.productCard {
  margin: 1rem;
  min-width: 50%;
}
</style>