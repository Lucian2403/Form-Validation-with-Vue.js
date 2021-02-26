<template>
  <form @submit.prevent="handleSubmit">
    <!-- v-model = store de value in {{here}} -->
    <label>Email:</label>
    <input type="email" required v-model="email">

    <label>Password:</label>
    <input type="password" required v-model="password">
    <div class="error" v-if="passwordError">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills (press alt + , to submit):</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div class="pill" v-for="skill in skills" :key="skill">
      <span @click="removeSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms">
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>

  </form>
  The submitted info will be in the console tab.
  <h4>Email: {{ email }}</h4>
  <h4>Password: {{ password }}</h4>
  <h4>Role: {{ role }}</h4>
  <h4>Skills: {{ skills }}</h4>
  <h4>Terms accepted: {{ terms }}</h4>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: 'designer',
      terms: false,
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(e) {
     if (e.key === ',' && this.tempSkill) {
       if (!this.skills.includes(this.tempSkill)) {
         this.skills.push(this.tempSkill)
       }
       this.tempSkill = ''
     }
    },
    removeSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item
      })
    },
    handleSubmit() {
      // validate password
      this.passwordError = this.password.length > 5 ?
      '' : 'Password must be at least 6 chars long'

      if(!this.passwordError) {
        console.log('email: ', this.email)
        console.log('password: ', this.password)
        console.log('role: ', this.role)
        console.log('skills: ', this.skills)
        console.log('terms accepted: ', this.terms)
      }
    }
  }
}
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
  box-shadow: 0px 5px 5px #ddd
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
input, select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
  outline: none;
}
input[type="checkbox"]{
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
.pill:hover {
  text-decoration: line-through;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
  outline: none;

  transition: .1s ease-in-out;
}
button:hover {
    background: #0a5fdd;
}
.submit {
  text-align: center;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: .8em;
  font-weight: bold;
}
</style>