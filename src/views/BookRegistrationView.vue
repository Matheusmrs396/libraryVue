<script>
import { mapState, mapStores, mapActions } from "pinia";
import { useProductStore } from "@/stores/product";
import { useCategoryStore } from "@/stores/category";
import { usePublisherStore } from "@/stores/publisher";
import { useAuthorStore } from "@/stores/author";
import { RouterLink } from "vue-router";

export default {
  components:{RouterLink},
  data() {
    return {
      currentProduct: {
        id: "",
        name: "",
        categoryId: "",
        image:"",
        price: "",
        amount:"",
        category: {},
      },
      editing: false,
    };
  },
  computed: {
    ...mapStores(useProductStore),
    ...mapState(useProductStore, ["products"]),
    ...mapState(useCategoryStore, ["categories"]),
    ...mapState(usePublisherStore, ["publishers"]),
    ...mapState(useAuthorStore, ["authors"]),
  },
  methods: {
    ...mapActions(useProductStore, [
      "getAllProducts",
      "saveProduct",
      "deleteProduct",
    ]),
    ...mapActions(useCategoryStore, ["getAllCategories"]),
    ...mapActions(useAuthorStore, ["getAllAuthors"]),
    ...mapActions(usePublisherStore, ["getAllPublishers"]),
    async save() {
      try {
        const msg = await this.saveProduct(this.currentProduct);
        alert(msg);
        this.editing = false;
        this.currentProduct = {};
      } catch (e) {
        alert("Ooops! Algo de errado!");
      }
    },
    async deleteItem(product_id) {
      try {
        await this.deleteProduct(product_id);
        alert("Item excluído com sucesso.");
      } catch (e) {
        alert(e);
      }
    },
    prepareToUpdate(product) {
      Object.assign(this.currentProduct, product);
      this.editing = true;
    },
  },
  async mounted() {
    try {
      await this.getAllCategories();
      await this.getAllAuthors();
      await this.getAllPublishers();
      await this.getAllProducts();
    } catch (e) {
      alert(e);
    }
  },
};
</script>
<template>
  <div class="title">
    <h4>Cadastro de Livros</h4>
  </div>
  <div class="product-form">
    <input type="text" v-model="currentProduct.name" placeholder="Título" />
    <select  v-model="currentProduct.categoryId" required>
      <option
        v-for="category in categories"
        :value="category.id"
        :key="category.id"
      >
        {{ category.description }}
      </option>
    </select>
    <select v-model="currentProduct.authorId" required>
      <option
        v-for="author in authors"
        :value="author.id"
        :key="author.id"
      >
        {{ author.name }}
      </option>
    </select>
    <select v-model="currentProduct.publisherId" required>
      <option
        v-for="publisher in publishers"
        :value="publisher.id"
        :key="publisher.id"
      >
        {{ publisher.name }}
      </option>
    </select>
    <input type="text" v-model="currentProduct.price" placeholder="Preço" />
    <input type="number" v-model="currentProduct.amount" placeholder="Quantidade" />
    <input type="text" v-model="currentProduct.image" placeholder="Link Imagem" />
    <button @click="save">
      {{ editing ? "Salvar" : "Adicionar" }}
    </button>
  </div>
  <div class="product-list">
    <table class="table">
      <thead>
        <tr>
          <th class="text-left">
            <span> <h5>ID</h5> </span>
          </th>
          <th class="text-left">
            <span> <h5>Descrição</h5> </span>
          </th>
          <th class="text-left">
            <span> <h5>Categoria</h5> </span>
          </th>
          <th class="text-left">
            <span> <h5>Autor</h5> </span>
          </th>
          <th class="text-left">
            <span> <h5>Editora</h5> </span>
          </th>
          <th class="text-left">
            <span> <h5>Preço</h5> </span>
          </th>
          <th class="text-left">
            <span> <h5>Imagem</h5> </span>
          </th>
          <th class="text-left">
            <span> <h5>Ações</h5> </span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product of products" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.category.description }}</td>
          <td>{{ product.author.name }}</td>
          <td>{{ product.publisher.name }}</td>
          <td>{{ product.price }}</td>
          <td>{{ product.image }}</td>
          <td>
          <q-card-actions>
            <q-btn @click="prepareToUpdate(product)" color="blue" icon="edit" label="Editar"></q-btn>
            <q-btn  @click="deleteItem(product.id)" color="red" icon="delete" label="Excluir"></q-btn>
          </q-card-actions>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.product-form input {
  width: 40%;
  height: 40px;
  border-radius: 20px;
  border: 1px solid gray;
  padding-left: 20px;
  font-size: 1.2em;
  margin-left: 1%;
}
.product-form select {
  width: 40%;
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
  display: flex;
  justify-content: space-between;
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