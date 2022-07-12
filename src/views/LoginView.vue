<script setup></script>

<template>
  <div class="login">
    <label for="email">E-mail</label>
    <input type="email">
    <label for="password">Senha</label>
    <input type="password">

    <button>Login</button>
  </div>
</template>

<style>
.login{
    width: 50vw;
    height: 50vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.login > input{
    border-radius: 5px;
    width: 50%;
}

.login > button{
    border-radius: 5px;
    padding: 0;
    margin: 3%;
    width: 50%;
}

</style>
