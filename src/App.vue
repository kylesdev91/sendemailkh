<template>
  <button @click="sendEmail">Email</button>
  <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <Products />
</template>

<script>
import axios from 'axios';
import Products from './views/Products.vue';
// import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'App',
  components: {
    Products,
  },
  methods: {
    sendEmail() {
      var content = this.items.reduce(function (a, b) {
        return a + '<tr><td>' + b.id + '</a></td><td>' + b.name + '</td></tr>';
      }, '');

      var formData = {
        emailSubject: 'Online Order',
        emailBody: content,
        orderTotal: 10,
      };
      axios
        .post(
          'https://sendemailkhfa.azurewebsites.net/api/sendmailwmsg',
          formData
        )
        .then((response) => {
          console.log(response);
        });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
