<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="toggleDetail">{{ project.title }}</h3>
      <div class="icons">
        <span @click="deleteProject" class="material-icons">delete</span>
        <span @click="" class="material-icons">edit</span>
        <span @click="toggleComplete" class="material-icons tick">done</span>
      </div>
    </div>
    <div class="details" v-if="showDetails">
      <p>{{ project.details }}</p>
      <div class="skillRequired">
        <strong>Skills Required : </strong
        ><span v-for="skill in project.SkillsRequired" :key="skill">
          {{ skill }} /
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      uri: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    toggleDetail() {
      this.showDetails = !this.showDetails;
    },
    deleteProject() {
      axios
        .delete(this.uri)
        .then(() => {
          this.$emit("remove", this.project.id);
        })
        .catch((err) => console.log(err.message));
    },
    toggleComplete() {
      axios
        .patch(this.uri, {
          complete: !this.project.complete,
        })
        .then(() => {
          this.$emit("complete", this.project.id);
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.skillRequired {
  margin: 20px 0;
}
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover {
  color: #777;
}
.project.complete {
  border-left: 4px solid #00ce89;
}

.project.complete .tick {
  color: #00ce89;
}
</style>