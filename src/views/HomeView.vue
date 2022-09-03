<template>
  <div class="home">
    <div v-if="projects.length">
      <div  v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @remove="removeProject(project.id)" @complete="completeProject(project.id)" />
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
  methods:{
    removeProject(id){
      this.projects = this.projects.filter((project) => {
        return project.id !== id
      });
    },
    completeProject(id){
     let temp = this.projects.find((project) => {
      return project.id === id
     });
     temp.complete = !temp.complete;
    }
  },
  mounted(){
     axios.get(' http://localhost:3000/projects')
     .then(res => this.projects = res.data)
     .catch(err => console.log(err.message));

  }
}
</script>

