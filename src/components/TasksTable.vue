<template>
  <Message :message="msg" />
  <div class="table-responsive">
    <table class="table table-striped table-sm table-hover">
      <thead class="thead-dark">
        <tr>
          <th>#</th>
          <th>Título</th>
          <th>Descrição</th>
          <th>Criado em</th>
          <th>Atualizado em</th>
          <th>Acções</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="task in tasks" :key="task.id">
          <td>{{ task.id }}</td>
          <td>{{ task.title }}</td>
          <td>{{ task.description }}</td>
          <td>{{ task.created_at }}</td>
          <td>{{ task.updated_at }}</td>
          <td id="actions">
            <button
              @click="$emit('editTask', { id: task.id })"
              class="btn btn-warning"
              id="btn-delete"
            >
              Editar
            </button>
            <button
              @click="$emit('deleteTask', { id: task.id })"
              class="btn btn-danger"
              id="btn-delete"
            >
              Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Message from "../components/Message.vue";

export default {
  name: "TasksTable",
  components: {
    Message,
  },
  props: {
    tasks: Array,
  },
  emits: ["deleteTask", "editTask"],
  data() {
    return {
      msg: null,
    };
  },
};
</script>

<style>
#btn-delete {
  margin-left: 10px;
}
</style>