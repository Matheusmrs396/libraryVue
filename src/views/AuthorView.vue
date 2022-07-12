<script>
import ListAuthor from "../components/author/ListAuthor.vue";
import FormAuthor from "../components/author/FormAuthor.vue";

export default {
  components: { ListAuthor, FormAuthor },
  data() {
    return {
      currentAuthor: {
        id: "",
        name: "",
      },
    };
  },

  methods: {
    prepareToUpdate(author) {
      Object.assign(this.currentAuthor, author);
    },
  },
};
</script>
<template>
  <h1>Cadastro de Autores</h1>
  <FormAuthor :currentAuthor="currentAuthor" />
  <ListAuthor @edit="prepareToUpdate" />
</template>

<style scoped></style>
