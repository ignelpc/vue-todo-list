<template>
  <div class="container">
    <div class="row my-3">
      <div class="col">
        <h2>Todas tarefas</h2>
      </div>
      <div class="col-2">
        <router-link to="/task" class="btn btn-primary"
          >Nova Tarefa</router-link
        >
      </div>
    </div>
    <section>
      <Message :message="msg" />
      <TasksTable
        @editTask="editTask"
        @deleteTask="deleteTask"
        :tasks="tasks"
      />
    </section>
  </div>
</template>

<script>
import Message from "../components/Message.vue";
import TasksTable from "../components/TasksTable.vue";

export default {
  name: "Home",
  components: {
    Message,
    TasksTable,
  },
  data() {
    return {
      tasks: [],
      msg: null,
    };
  },
  methods: {
    editTask(payload) {
      this.$router.push({ name: "Task", params: { id: payload.id } });
    },
    async getTasks() {
      const response = await fetch("http://localhost:3000/tasks");
      const data = await response.json();

      this.tasks = data;
    },
    deleteTask(payload) {
      fetch(`http://localhost:3000/tasks/${payload.id}`, {
        method: "DELETE",
      }).then((response) => {
        if (response.ok) {
          this.msg = "Tarefa eliminada com sucesso";
          setTimeout(() => (this.msg = null), 2000);

          this.getTasks();
        } else {
          this.msg = "Não foi possível eliminar a tarefa";
          setTimeout(() => (this.msg = null), 2000);
        }
      });
    },
  },
  mounted() {
    this.getTasks();
  },
};
</script>

<style>
#btn-delete {
  margin-left: 10px;
}
</style>
