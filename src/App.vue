<template>
  <nav>
    <router-link :to="{ name: 'home' }">All Projects</router-link>
    <router-link :to="{ name: 'add-project' }">Add a New Project</router-link>
  </nav>
  <router-view />
</template>

<style>
body {
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: #555;
}
nav {
  display: flex;
  justify-content: center;
}
nav a {
  margin: 10px 40px;
  text-decoration: none;
  color: #777;
  font-size: 24px;
  opacity: 0.5;
}
nav a:active{
  border-bottom: 4px solid #00ce89;
}
</style>
