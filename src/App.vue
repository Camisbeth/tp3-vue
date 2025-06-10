<template>
  <div id="app">
    <nav>
      <router-link to="/">Formulario</router-link> |
      <router-link to="/usuarios">Usuarios</router-link>
    </nav>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f1f1f1;
  background-color: #121212;
  min-height: 100vh;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #f1f1f1;
  text-decoration: none;
  margin: 0 10px;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
