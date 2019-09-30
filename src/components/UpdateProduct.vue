<template>
  <div>
    <b-button @click="modalShow = !modalShow" variant="info">
      <i class="far fa-edit"></i>
    </b-button>
    <b-modal
      v-model="modalShow"
      title="Update Product"
      @show="showModal"
      @hidden="hideModal"
      @ok="handleSubmit"
    >
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
          <b-form-radio v-model="form.inventoryStatus" name="inventoryStatus" value="true">In stock</b-form-radio>
          <b-form-radio
            v-model="form.inventoryStatus"
            name="inventoryStatus"
            value="false"
          >On Backorder</b-form-radio>
        </b-form-group>
      </b-form>
    </b-modal>
  </div>
</template>
<script>
export default {
  name: "UpdateProduct",
  data() {
    return {
      modalShow: false,
      form: {
        name: "",
        price: "",
        brand: "",
        inventoryStatus: ""
      },
      submitted: false
    };
  },
  props: ["product"],
  methods: {
    showModal() {
      console.log("Modal Opened");
      this.form = {
        name: this.$props.product.name,
        price: this.$props.product.price.split("$")[1],
        brand: this.$props.product.brand,
        inventoryStatus: this.$props.product.inventoryStatus.toString()
      };
    },
    hideModal() {
      console.log("Modal Closed");
    },
    handleSubmit() {
      console.log("Submitted");
      this.$emit("updateProduct", {
        name: this.form.name,
        price: "$" + this.form.price,
        brand: this.form.brand,
        inventoryStatus: this.form.inventoryStatus === "true",
        id: this.$props.product.id
      });
    }
  }
};
</script>
<style scoped lang="scss">
</style>