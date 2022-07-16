<script>
import { mapActions } from "pinia";
import { useCategoryStore } from "@/stores/category";
import { useProductStore } from "../../stores/product";

export default {
  props: {
    currentProduct: {
      type: Object,
    },
  },
  data() {
    return {
      product: this.currentProduct,
      category: this.currentCategory,
    };
  },
  methods: {
    ...mapActions(useProductStore, ["saveProduct"]),
    ...mapActions(useCategoryStore, ["getAllCategories"]),
    async save() {
      try {
        const msg = await this.saveProduct(this.product);
        alert(msg);
        Object.assign(this.product, {
          id: "",
          description: "",
        });
      } catch (e) {
        alert("Ooops! Algo de errado!");
      }
    },
  },
};
</script>

<template>
  <div class="product-form">
    <input type="text" v-model="product.name" />
    <input type="text" v-model="product.price" />
    <input type="text" v-model="product.image" />
    <select v-model="product.categoryId">
      <option
        v-for="category in product.category.id"
        :value="category.id"
        :key="category.id"
      >
        {{ category.description }}
      </option>
    </select>



    <button @click="save">
      {{ currentProduct.id !== "" ? "Salvar" : "Adicionar" }}
    </button>
  </div>
</template>

<style scoped>
.product-form input {
  width: 75%;
  height: 40px;
  border-radius: 20px;
  border: 1px solid gray;
  padding-left: 20px;
  font-size: 1.2em;
}

.product-form button {
  height: 35px;
  width: 20%;
  margin-left: 2%;
  background-color: rgb(63, 63, 125);
  color: whitesmoke;
  font-size: 1.2em;
  border-radius: 20px;
  border: 0;
}

.product-form {
  margin: 3% auto;
  width: 70%;
}
</style>
