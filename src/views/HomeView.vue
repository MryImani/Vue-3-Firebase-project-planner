<template>
  <div class="home">
    <div v-if="projects.length">
      <div  v-for="project in projects" :key="project.id">
        <SingleProject :project="project" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import SingleProject from '../components/SingleProject.vue'
export default {
  name: 'HomeView',
  components: {
    SingleProject
  },
  data(){
    return {
      projects : []
    }
  },
  mounted(){
     axios.get(' http://localhost:3000/projects')
     .then(res => this.projects = res.data)
     .catch(err => console.log(err.message));

  }
}
</script>
