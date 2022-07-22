<template>
  <div>
    <button @click="sendEmail">Email w POST</button>
    <button @click="sendEmailGet">Email w GET</button>
  </div>
  <h2>{{ product.id }}</h2>
  <h2>{{ product.name }}</h2>
</template>

<script>
import axios from 'axios';
import items from '../data/items';

export default {
  props: ['product'],
  data() {
    return {
      items: items,
      message: '',
    };
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
        .post('https://sendemailkhfa.azurewebsites.net/api/sendmail', formData)
        .then((response) => {
          console.log(response);
        });
    },
    sendEmailGet() {
      axios
        .get('https://sendemailkhfa.azurewebsites.net/api/mail')
        .then((response) => {
          console.log(response);
        });
    },
  },
};
</script>
