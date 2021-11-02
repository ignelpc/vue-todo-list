<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark" id="nav">
    <router-link to="/" class="navbar-brand">
        <img :src="logo" id="logo" :alt="alt">
    </router-link>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav">
      <li class="nav-item active">
        <router-link to="/" class="nav-link">Home</router-link>
      </li>
      <li class="nav-item">
        <router-link to="/task" class="nav-link">Criar Tarefa</router-link>
      </li>
    </ul>
  </div>
  </nav>
</template>

<script>
    export default {
        name: 'Navbar',
        props: ["logo", "alt"]
    }
</script>

<style scoped>
/* #nav {
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;   
    align-items: center;
}

#logo-url {
    margin: auto;
    margin-left: 0;
}

#logo {
    width: 40px;
    height: 40px;
}

#nav a {
    color: rgb(180, 15, 15);
    text-decoration: none;
    margin: 12;
    transition: .5s;
}

#nav a:hover {
    color: darkgoldenrod
} */
</style>