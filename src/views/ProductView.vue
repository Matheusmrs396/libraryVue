<script>
import { mapState, mapStores, mapActions } from "pinia";
import { useProductStore } from "@/stores/product";
import { useCategoryStore } from "@/stores/category";
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
        category: {},
      },
      editing: false,
    };
  },
  computed: {
    ...mapStores(useProductStore),
    ...mapState(useProductStore, ["products"]),
    ...mapState(useCategoryStore, ["categories"]),
  },
  methods: {
    ...mapActions(useProductStore, ["getAllProducts"]),
    ...mapActions(useCategoryStore, ["getAllCategories"]),
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
  <div class="top">
    <h3>Livros Cadastrados</h3>
    <q-btn to="/cadastroLivro" color="green" icon="add" label="Cadastrar Livro"/>
  </div>
 <br>
  <div class="main">
    <q-card class="my-card justify" style="width: 30vw; height: 30vh; margin: 1%;" v-for="product of products" :key="product.id">
          <q-card-section horizontal>
            <q-img
              class="col-5"
              src="https://cdn.quasar.dev/img/parallax1.jpg"
            />

            <q-card-section>
            
            <tr> Nome: {{ product.name }}</tr>
            <tr> Preço: {{ product.price }} </tr>
            <tr>Categoria: {{ product.category.description }}</tr>
            </q-card-section>
          </q-card-section>

          <q-separator />

          <q-card-actions>
            <q-btn to="/cadastroLivro" color="blue" icon="edit" label="Editar"></q-btn>
            <q-btn  to="/cadastroLivro" color="red" icon="delete" label="Excluir"></q-btn>
          </q-card-actions>
    </q-card>
  </div>
</template>

<style scoped>
.main{
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.top{
  display: flex;
  justify-content: space-between;

}
</style>
