<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div class="error" v-if="passwordError">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills (press alt + comma to add skill)</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="removeSkill(skill)">
        {{ skill }}
      </span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditions</label>
    </div>

    <!-- <div>
      <input type="checkbox" value="apple" v-model="names" />
      <label>Apple</label>
      <input type="checkbox" value="banana" v-model="names" />
      <label>Banana</label>
      <input type="checkbox" value="mango" v-model="names" />
      <label>Mango</label>
    </div> -->

    <div class="submit">
      <input type="submit" value="Create an Account" />
    </div>
  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms: {{ terms }}</p>
  <!-- <p>Fruits: {{ names }}</p> -->
</template>

<script>
export default {
  data() {
    return {
      email: "admin",
      password: "",
      role: "designer",
      terms: false,
      //   names: [],
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    removeSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handleSubmit() {
      //   console.log("form submitted");
      this.passwordError =
        this.password.length >= 7 ? "" : "Password must at least 8 characters.";

      if (!this.passwordError) {
        console.log("Email: ", this.email);
        console.log("Password: ", this.password);
        console.log("Role: ", this.role);
        console.log("Skills: ", this.skills);
        console.log("Terms: ", this.terms);
      }
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background-color: #fff;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  padding: 10px 6px;
  display: block;
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
  padding: 6px 10px;
  background-color: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
input[type="submit"] {
  background-color: #0b6dff;
  margin-top: 20px;
  color: #fff;
  border-radius: 20px;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>