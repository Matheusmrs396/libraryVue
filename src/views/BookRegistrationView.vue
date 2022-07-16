<script>
import ListProduct from "../components/product/ListProduct.vue";
import FormProduct from "../components/product/FormProduct.vue";

export default {
  components:{ListProduct,FormProduct},
  data() {
    return {
      currentProduct: {
        id: "",
        name: "",
        categoryId: "",
        price:"",
        image:"",
        category: {},
      },
    };
  },

  methods: {
    prepareToUpdate(product) {
      Object.assign(this.currentProduct, product);
      this.editing = true;
    },
  }
};
</script>
<template>
  <h3>Cadastro de livros</h3>
  <FormProduct :currentProduct="currentProduct" />
  <ListProduct @edit="prepareToUpdate" />
</template>

<style scoped>
.product-form input {
  width: 40%;
  height: 40px;
  border-radius: 20px;
  border: 1px solid gray;
  padding-left: 20px;
  font-size: 1.2em;
}
.product-form select {
  width: 30%;
  height: 40px;
  border-radius: 20px;
  border: 1px solid gray;
  padding-left: 20px;
  font-size: 1.2em;
  margin-left: 1%;
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
.product-list,
.product-form {
  margin: 3% auto;
  width: 70%;
}
table {
  /* display: table; */
  border-collapse: separate;
  border-spacing: 2px;
  border-color: gray;
  width: 100%;
}
th {
  border-bottom: 2px solid #444;
  text-align: left;
}
td {
  padding: 10px;
}
thead tr {
  background-color: #444;
  color: whitesmoke;
}
tbody tr:nth-child(odd) {
  background-color: #c3c3c3;
}
</style>