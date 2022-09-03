<template>
  <form @submit.prevent="handelSubmit()">
    <label>Title:</label>
    <input type="text" name="" id="" v-model="title" required />
    <label>Details:</label>
    <textarea
      name=""
      id=""
      cols="30"
      rows="10"
      v-model="details"
      required
    ></textarea>
    <label>Skills Required:</label>
    <input type="text" v-model="tempSkills" @keyup="addSkill" />

    <div class="skills" v-if="skills">
      <span
        class="skill"
        v-for="skill in skills"
        :key="skill"
        @click="removeSkill(skill)"
        >{{ skill }}</span
      >
    </div>
    <div class="submit">
      <button>Add Project</button>
    </div>
  </form>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      title: "",
      details: "",
      tempSkills: [],
      skills: [],
    };
  },
  methods: {
    addSkill(e) {
      if (
        (e.key === "," || e.key === "-" || e.key === " ") &&
        this.tempSkills
      ) {
        let tempskill = this.tempSkills;
        let skill = tempskill.substr(0, tempskill.length - 1);
        if (!this.skills.includes(skill)) {
          this.skills.push(skill);
        }
        this.tempSkills = "";
      }
    },
    removeSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handelSubmit() {
      axios
        .post("http://localhost:3000/projects", {
        id: '',
          title: this.title,
          details: this.details,
          SkillsRequired: this.skills,
          complete: false,
        })
        .then(() => {
          console.log("add a new project successfull");
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style scoped>
form {
  max-width: 26.25rem;
  margin: 1.875rem auto;
  background: #fff;
  text-align: left;
  padding: 2.5rem;
  border-radius: 0.625rem;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 1.562rem 0 0.937rem;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
textarea {
  display: block;
  padding: 0.625rem 0.375rem;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 1rem;
  margin: 0 0.625rem 0 0;
  position: relative;
  top: 2px;
}
.skills {
  margin: 1.562rem 0 0.937rem;
}
.skill {
  margin-right: 15px;
  padding: 10px;
  background: #eee;
  border-radius: 5px;
  text-align: center;
  font-weight: bold;
  font-size: 12px;
  cursor: pointer;
  color: #777;
  letter-spacing: 1px;
}
.submit {
  text-align: center;
}
button {
  background: #00ce89;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: #fff;
  border-radius: 10px;
  cursor: pointer;
}
</style>