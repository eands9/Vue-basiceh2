<template>
  <button @click="showMsg">Show Message</button>
  {{ message }}
  <button @click="sendmail">Send Mail</button>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from "axios";

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      message: ""
    };
  },
  methods: {
    async showMsg(){
      // const { text } = await (await fetch("/api/message")).json();
      // const { text } = axios.get("/api/message").then((response) => {
      //   console.log(response.data.text)
      // })
      axios.get("/api/message").then((response) => {
        console.log(response.data.text)
        this.message=response.data.text
      })
      // this.message = text;
    },
    async sendmail(){
      axios.get("/api/sendmail").then((response) => {
        console.log(response)
      })
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
