<template>
  <div class="home">
    <FilterNavProject :current="current" @filterProject="current = $event" @click="filteredProjects"/>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @remove="removeProject(project.id)"
          @complete="completeProject(project.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

import SingleProject from "../components/SingleProject.vue";
import FilterNavProject from "../components/FilterNavProject.vue";
export default {
  name: "HomeView",
  components: {
    SingleProject,
    FilterNavProject,
  },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  methods: {
    removeProject(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },
    completeProject(id) {
      let temp = this.projects.find((project) => {
        return project.id === id;
      });
      temp.complete = !temp.complete;
    },
    
  },
  mounted() {
    axios
      .get(" http://localhost:3000/projects")
      .then((res) => (this.projects = res.data))
      .catch((err) => console.log(err.message));
  },
  computed:{
    filteredProjects() {
       if (this.current === "completed") {
        return this.projects.filter((project) => project.complete);
      }
       if (this.current === "ongoing") {
        return this.projects.filter((project) => !project.complete );
      }
      return this.projects
    },
  }
};
</script>

