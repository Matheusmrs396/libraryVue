<script>
import { mapActions } from "pinia";
import { useAuthorStore } from "@/stores/author";

export default {
  props: {
    currentAuthor: {
      type: Object,
    },
  },
  data() {
    return {
      author: this.currentAuthor,
    };
  },
  methods: {
    ...mapActions(useAuthorStore, ["saveAuthor"]),
    async save() {
      try {
        const msg = await this.saveAuthor(this.author);
        alert(msg);
        Object.assign(this.author, {
          id: "",
          name: "",
        });
      } catch (e) {
        alert("Ooops! Algo de errado!");
      }
    },
  },
};
</script>

<template>
  <div class="author-form">
    <q-input rounded outlined style="height:40px; width:40%" v-model="author.name" type="text" label="Nome do Autor" />
    <button @click="save">
      {{ currentAuthor.id !== "" ? "Salvar" : "Adicionar" }}
    </button>
  </div>
</template>

<style scoped>
.author-form input {
  width: 40%;
  height: 40px;
  border-radius: 20px;
  border: 1px solid gray;
  padding-left: 20px;
  font-size: 1.2em;
}

.author-form button {
  height: 35px;
  width: 20%;
  margin-left: 2%;
  background-color: rgb(63, 63, 125);
  color: whitesmoke;
  font-size: 1.2em;
  border-radius: 20px;
  border: 0;
}

.author-form {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 3% auto;
  width: 70%;
}
</style>
