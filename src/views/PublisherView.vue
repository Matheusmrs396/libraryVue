<script>
import ListPublisher from "../components/publisher/ListPublisher.vue";
import FormPublisher from "../components/publisher/FormPublisher.vue";

export default {
  components: { ListPublisher, FormPublisher },
  data() {
    return {
      currentPublisher: {
        id: "",
        name: "",
        link: "",
      },
    };
  },

  methods: {
    prepareToUpdate(publisher) {
      Object.assign(this.currentPublisher, publisher);
    },
  },
};
</script>
<template>
  <h3>Cadastro de Editoras</h3>
  <FormPublisher :currentPublisher="currentPublisher" />
  <ListPublisher @edit="prepareToUpdate" />
</template>

<style scoped></style>
