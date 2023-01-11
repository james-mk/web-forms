<template>
  <form>
    <label>Email</label>
    <input type="email" v-model="email" required />
    <label>Password</label>
    <input type="password" v-model="password" required />
    <label>Role</label>
    <select v-model="role" required>
      <option value="developer">Web Developer</option>
      <option value="designer">Graphic Designer</option>
    </select>
    <div>
      <input type="checkbox" value="html" v-model="skills" />
      <label>Html</label>
    </div>
    <div>
      <input type="checkbox" value="css" v-model="skills" />
      <label>Css</label>
    </div>
    <div>
      <input type="checkbox" value="javascript" v-model="skills" />
      <label>Javascript</label>
    </div>

    <div class="otherSkills">
      <label>Other Skills</label>
      <input type="text" v-model="otherSkills" @keyup="addSkill" />
    </div>
    <div v-for="otherskill in otherSkillsArray" :key="otherskill" class="pill">
      <span @click="deleteSkill(otherskill)"> {{ otherskill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>Accept terms and conditions</label>
    </div>
  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Skills: {{ skills }}</p>

  <p>Accept Terms: {{ terms }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      skills: [],
      otherSkillsArray: [],
      otherSkills: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key == "," && this.otherSkills) {
        if (!this.otherSkillsArray.includes(this.otherSkills)) {
          this.otherSkillsArray.push(this.otherSkills);
        }
        this.otherSkills = "";
      }
    },
    deleteSkill(otherskill) {
      this.otherSkillsArray = this.otherSkillsArray.filter((item) => {
        return otherskill !== item;
      });
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
</style>