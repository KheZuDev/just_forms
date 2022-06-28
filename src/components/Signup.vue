<template>
  <form @submit.prevent="submit">
    <label for="Email">Email</label>
    <input type="email" required v-model="email" />
    <label for="">Password</label>
    <p v-if="errmessage" style="color: red">{{ errmessage }}</p>
    <input type="password" required v-model="password" />
    <label for=" Roles: ">Roles - {{ role }}</label>

    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
      <option value="engineer">Web Engineer</option>
    </select>

    <div>
      <label for="">Skills</label>
      <input type="text" @keyup.alt="addSkills" v-model="skill" />
    </div>
    <div v-for="skill in skills" :key="skill">
      <p>
        {{ skill }}
        <span class="cross" @click="deleteSkill(skill)">&#x2716;</span>
      </p>
    </div>
    <div>
      <input type="checkbox" v-model="accept" />
      <label for="">Accept terms and conditions</label>
    </div>
    <div class="align">
      <button class="create">Create account</button>
    </div>
  </form>
  <p>email - {{ email }}</p>
  <p>password -{{ password }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      accept: false,
      skills: [],
      skill: "",
      errmessage: "",
    };
  },
  methods: {
    addSkills(e) {
      if (e.key === "," && this.skill) {
        this.skills.push(this.skill);
        this.skill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((loopSkill) => {
        return loopSkill != skill;
      });
    },
    submit() {
      if (this.password.length < 8) {
        this.errmessage = "Passwrod must be ateleat 8 charractoers";
      }
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
.cross {
  cursor: pointer;
  color: red;
}
.create {
  padding: 8px;
  background-color: royalblue;
  color: white;
  border-radius: 10px;
  border-color: white;
}
.align {
  text-align: center;
}
</style>