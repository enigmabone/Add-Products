<template>
  <b-col md="4" class="m-3">
    <b-card header="Add Product">
      <b-card-body>
        <b-form autocomplete="off">
          <b-form-group label="Name">
            <b-form-input v-model="form.name" id="name" name="name" trim></b-form-input>
          </b-form-group>

          <b-form-group label="Price ($)">
            <b-form-input v-model="form.price" id="price" name="price" trim></b-form-input>
          </b-form-group>

          <b-form-group label="Brand">
            <b-form-input v-model="form.brand" id="brand" name="brand" trim></b-form-input>
          </b-form-group>

          <b-form-group label="Inventory">
            <b-form-radio
              v-model="form.inventoryStatus"
              name="inventoryStatus"
              value="true"
            >In stock</b-form-radio>
            <b-form-radio
              v-model="form.inventoryStatus"
              name="inventoryStatus"
              value="false"
            >On Backorder</b-form-radio>
          </b-form-group>
        </b-form>
      </b-card-body>

      <b-button block variant="primary" @click="addProduct">Add Product</b-button>
    </b-card>
  </b-col>
</template>
<script>
import { required } from "vuelidate/lib/validators";
export default {
  name: "AddProduct",
  data() {
    return {
      form: {
        name: "",
        price: "",
        brand: "",
        inventoryStatus: ""
      },
      submitted: false
    };
  },
  methods: {
    addProduct() {
      this.submitted = true;
      this.$emit("addProduct", {
        name: this.form.name,
        price: "$" + this.form.price,
        brand: this.form.brand,
        inventoryStatus: this.form.inventoryStatus === "true"
      });
      this.form = {
        name: "",
        price: "",
        brand: "",
        inventoryStatus: ""
      };
      this.submitted = false;
      console.log(this.form);
    }
  },
  validations: {
    name: {
      required
    },
    price: {
      required
    },
    brand: {
      required
    }
  }
};
</script>
<style scoped lang="scss">
</style>