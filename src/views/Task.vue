<template>
  <div class="container">
    <div class="row my-3">
      <div class="col">
        <h2>{{ action }} Tarefa</h2>
      </div>
      <div class="col-2">
        <router-link to="/" class="btn btn-primary px-5">Voltar</router-link>
      </div>
    </div>
    <Message :message="msg" />
    <div class="card border-primary">
      <div class="card-body">
        <form @submit.prevent="verify">
          <div class="form-group mb-3">
            <label for="title">Título</label>
            <input
              type="text"
              class="form-control"
              name="title"
              id="title"
              placeholder="Digite o título da tarefa"
              v-model="title"
            />
          </div>
          <div class="form-group mb-3">
            <label for="description">Descrição</label>
            <input
              type="text"
              class="form-control"
              name="description"
              id="description"
              placeholder="Digite o descrição da tarefa"
              v-model="description"
            />
          </div>
          <div class="col mt-2">
            <button class="btn btn-success px-5">{{ action }}</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import Message from "../components/Message.vue";

export default {
  name: "Task",
  components: {
    Message,
  },
  data() {
    return {
      task: {},
      title: "",
      description: "",
      action: "Cadastrar",
      msg: "",
    };
  },
  methods: {
    formatedDate(date = new Date()) {
      let day = date.getDate();
      let month = date.getMonth() + 1;
      let year = date.getFullYear();
      let hour = date.getHours();
      let minutes = date.getMinutes();
      let seconds = date.getSeconds();

      if (day.toString().length === 1) day = "0" + day;
      if (month.toString().length === 1) month = "0" + month;

      return year + "/" + month + "/" + day+" "+hour+":"+minutes+":"+seconds;
    },
    async getTask(id) {
      const response = await fetch(`http://localhost:3000/tasks/${id}`);
      const data = await response.json();
      if (response.ok) {
        this.title = data.title;
        this.description = data.description;
        this.action = "Atualizar";
      }
    },
    verify() {
      this.action === "Cadastrar" ? this.createTask() : this.updateTask();
    },
    async createTask() {
      const data = {
        title: this.title,
        description: this.description,
        created_at: this.formatedDate(),
        updated_at: this.formatedDate(),
      };

      const dataJson = JSON.stringify(data);

      const response = await fetch("http://localhost:3000/tasks", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: dataJson,
      });

      if (!response.ok) {
        this.msg = "Falha ao cadastrar a tarefa";
        setTimeout(() => (this.msg = ""), 2000);
        return false;
      }

      this.msg = "Tarefa cadastrada com sucesso!";
      setTimeout(() => (this.msg = ""), 2000);

      this.clearFiels();
    },
    async updateTask() {
      const data = {
        title: this.title,
        description: this.description,
        updated_at: this.formatedDate(),
      };

      const dataJson = JSON.stringify(data);

      const response = await fetch(`http://localhost:3000/tasks/${this.$route.params.id}`, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: dataJson,
      });

      if (!response.ok) {
        this.msg = "Falha ao atualizar tarefa";
        setTimeout(() => (this.msg = ""), 2000);
        return false;
      }

      this.msg = "Tarefa atualizada com sucesso!";
      setTimeout(() => (this.msg = ""), 2000);

      this.clearFiels();
    },
    clearFiels() {
      this.title = "";
      this.description = "";
    },
  },
  mounted() {
    if (this.$route.params.id) this.getTask(this.$route.params.id);
  },
};
</script>