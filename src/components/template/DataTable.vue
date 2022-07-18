<script>
export default {
  props: {
    columns: {
      type: Array,
      required: true,
    },
    items: {
      type: Array,
      required: true,
    },
  },
};
</script>
<template>
  <table class="data-table">
    <thead>
      <tr>
        <th class="text-left" v-for="column of columns" :key="column.field">
          <span>
            <h6>{{ column.label }}</h6>
          </span>
        </th>
        <th class="text-left">
          <span> <h6>Ações</h6> </span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(row, i) of items" :key="i">
        <!-- <td v-for="(data, i) of row" :key="i">{{ data }}</td> -->
        <td v-for="column of columns" :key="column.field">
          <span v-if="column.href">
            <a :href="row[column.field]" target="_blank">
              {{ row[column.field] }}</a
            >
          </span>
          <span v-else>
            {{ row[column.field] }}
          </span>
        </td>
        <td>
          <q-card-actions>
            <q-btn  @click="$emit('edit', row)" color="blue" icon="edit" label="Editar"></q-btn>
            <q-btn   @click="$emit('delete', row)" color="red" icon="delete" label="Excluir"></q-btn>
          </q-card-actions>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
a {
  color: inherit;
}
.data-table {
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
