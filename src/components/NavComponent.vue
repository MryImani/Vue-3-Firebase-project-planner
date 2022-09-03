<template>
    <nav>
    <router-link :to="{ name: 'home' }">All Projects</router-link>
    <router-link :to="{ name: 'add-project' }">Add a New Project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style scoped>
nav {
  display: flex;
  justify-content: center;
}
nav a {
  margin: 10px 40px;
  text-decoration: none;
  color: #999;
  font-size: 18px;
}
a.router-link-active{
  border-bottom: 4px solid #00ce89;
  padding-bottom: 4px;
}
</style>