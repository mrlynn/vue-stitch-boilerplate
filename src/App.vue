<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
    <div id="auth-status">Logged Out</div>
  </div>
</template>

<script>
import { Stitch, AnonymousCredential } from 'mongodb-stitch-browser-sdk'
var util = require('util')
console.log(util.inspect(Stitch))

export default {
  name: 'App',
  data() {
    return {
      events: [],
      errors: []
    }
  },
  created() {
    const client = Stitch.initializeDefaultAppClient('stitch-sheets-zkvuv');
    client.auth.loginWithCredential(new AnonymousCredential()).then(user => {
      document.getElementById('auth-status').innerHTML = 
        `Logged in as anonymous user with id ${user.id}`;
    });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
