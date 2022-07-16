<script>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header>
    <RouterLink to="/"> Home</RouterLink> |
    <RouterLink to="/categorias"> Categorias</RouterLink> |
    <RouterLink to="/produtos"> Livros</RouterLink> |
    <RouterLink to="/autores"> Autor</RouterLink> |
    <RouterLink to="/editoras"> Editora</RouterLink>
  </header>
  <main>
    <RouterView />
  </main>
</template>

<style>
@import "@/assets/base.css";

#app {
  height: 100vh;
}

header {
  width: 100vw;
  height: 10%;
  background-color: black;
  color: whitesmoke;
  font-size: 1em;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}

main {
  padding: 0;
}
.title{
  display: flex;
  justify-content: center;
  margin: 1%;
}

</style>
