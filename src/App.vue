<template>
  <nav>
    <router-link to="/">Home</router-link> | 
    <router-link to="/add">Add</router-link>
  </nav>
  <router-view/>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #2c3e50;
}

nav {
  color: white;
  text-align: center;
  margin-bottom: 25px;
}

a {
  font-weight: bold;
  color: white;
  text-decoration: none;
}

.router-link-exact-active {
  border-bottom: 2px solid green;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #000;
  max-width: 600px;
  margin: 25px auto;
}
</style>
