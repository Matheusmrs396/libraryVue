<script>
import { mapState, mapStores, mapActions } from "pinia";
import { useProductStore } from "@/stores/product";
import { useCategoryStore } from "@/stores/category";
import DataTable from "../template/DataTable.vue";

export default {
  components:{DataTable},
  data() {
    return {
      columns: [
        { label: "ID", field: "id" },
        { label: "Nome", field: "name" },
        { label: "Categoria", field: "categoryId" },
        { label: "Preço", field: "price" },
        { label: "Imagem", field: "image" }
      ],
    };
  },

  computed: {
    ...mapStores(useProductStore),
    ...mapState(useProductStore, ["products"]),
    ...mapState(useCategoryStore, ["categories"]),
  },
  methods: {
    ...mapActions(useProductStore, [
      "getAllProducts",
      "saveProduct",
      "deleteProduct",
    ]),
    ...mapActions(useCategoryStore, ["getAllCategories"]),
 //   async save() {
   //   try {
     //   const msg = await this.saveProduct(this.currentProduct);
     //   alert(msg);
     //   this.editing = false;
     //   this.currentProduct = {};
     // } catch (e) {
       // alert("Ooops! Algo de errado!");
      //}
  //  },
    async deleteItem(product_id) {
      try {
        await this.deleteProduct(product_id);
        alert("Item excluído com sucesso.");
      } catch (e) {
        alert(e);
      }
    },
    //prepareToUpdate(product) {
     // Object.assign(this.currentProduct, product);
     // this.editing = true;
    //},
  },
  async mounted() {
    try {
      await this.getAllCategories();
      await this.getAllProducts();
    } catch (e) {
      alert(e);
    }
  },
};
</script>
<template>
  <div class="product-list">
    <data-table
      :columns="columns"
      :items="products"
      @edit="$emit('edit', $event)"
      @delete="deleteItem"
    />
  </div>
</template>
<style scoped>
.product-list {
  margin: 3% auto;
  width: 70%;
}
</style>