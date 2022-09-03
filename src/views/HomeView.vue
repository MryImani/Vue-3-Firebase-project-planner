<template>
  <div class="home">
    <div v-if="projects.length">
      <div class="project" v-for="project in projects" :key="project.id">
        <p>{{project.title}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HomeView',
  components: {
  },
  data(){
    return {
      projects : [],
    }
  },
  mounted(){
     axios.get(' http://localhost:3000/projects')
     .then(res => this.projects = res.data)
     .catch(err => console.log(err.message));

  }
}
</script>
