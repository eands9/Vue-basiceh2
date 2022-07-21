<template>
  <button @click="showMsg">Show Message</button>
  {{ message }}
  <button @click="sendmail">Send Mail</button>
  <button @click="sendmailWMsg">Send Mail w Message</button>
  <Products 
    v-for="product in items"
    :key="product.id"
    :product="product"
  />

</template>

<script>
import axios from "axios";
import Products from '@/components/Products.vue'
import items from '@/data/items.js';

export default {
  name: 'App',
  components:{
    Products
  },
  data() {
    return {
      items: items,
      message: "",

    };
  },
  methods: {
    // axios ref https://www.koderhq.com/tutorial/vue/http-axios/#api
    async showMsg(){
      axios.get("/api/message").then((response) => {
        console.log(response.data.text)
        this.message=response.data.text
      })
    },
    async sendmail(){
      axios.get("https://vue-emailfa.azurewebsites.net/api/sendmail").then((response) => {
        console.log(response)
      })
    },
    async sendmailWMsg(){
      var content = this.items.reduce(function(a,b){
        return a + '<tr><td>' + b.id + '</a></td><td>' + b.name + '</td></tr>'
      },'')

      var formData = {
        emailSubject: "Online Order",
        // emailBody: "This is the passed email body"
        emailBody: content
      }

      // .post("/api/sendmailwmsg",formData)
      axios
        .post("https://vue-emailfa.azurewebsites.net/api/sendmailwmsg",formData)
        .then((response) => {console.log(response)})
    }
  }
}
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

