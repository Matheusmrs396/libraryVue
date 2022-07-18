<script>
import { mapActions } from "pinia";
import { usePublisherStore } from "@/stores/publisher";

export default {
  props: {
    currentPublisher: {
      type: Object,
    },
  },
  data() {
    return {
      publisher: this.currentPublisher,
    };
  },
  methods: {
    ...mapActions(usePublisherStore, ["savePublisher"]),
    async save() {
      try {
        const msg = await this.savePublisher(this.publisher);
        alert(msg);
        Object.assign(this.publisher, {
          id: "",
          name: "",
          link: "",
        });
      } catch (e) {
        alert("Ooops! Algo de errado!");
      }
    },
  },
};
</script>

<template>
  <div class="publisher-form">
    <q-input rounded outlined style="height:40px; width:40%; margin: 1%;" v-model="publisher.name" type="text" label="Nome da Editora" />
    <q-input rounded outlined style="height:40px; width:40%" v-model="publisher.link" type="text" label="Link do Site" />
    <button @click="save">
      {{ currentPublisher.id !== "" ? "Salvar" : "Adicionar" }}
    </button>
  </div>
</template>

<style scoped>
.publisher-form input {
  width: 75%;
  height: 40px;
  border-radius: 20px;
  border: 1px solid gray;
  padding-left: 20px;
  font-size: 1.2em;
}

.publisher-form button {
  height: 35px;
  width: 20%;
  margin-left: 2%;
  background-color: rgb(63, 63, 125);
  color: whitesmoke;
  font-size: 1.2em;
  border-radius: 20px;
  border: 0;
}

.publisher-form {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 3% auto;
  width: 70%;
}
</style>
