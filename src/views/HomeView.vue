<script>
export default {
  data() {
    return {
      form: {
        'email': 'joyywamaitha@gmail.com',
        'password': 'wamaitha@2022'
      }
    }
  },
  methods: {
    actionLogin(){
      console.log("Logged in")
      this.$router.push({ path: '/about' })
    }
  }
}
</script>

<template>
  <div id="mystyle">
    <h1>Log in</h1>
    <label for="email">Email</label>
    <input type="email" id="email" v-model="form.email"/>

    <br/>

    <label for="password">Password</label>
    <input type="password" id="password" v-model="form.password"/>

    <br/>

    <button v-on:click="actionLogin">Log In</button>

  </div>
</template>
<style>
.template{
  background-color: #E6E6FA;
}
</style>