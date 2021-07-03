<template>
  <!-- <div id="app">
  <img v-bind:src="picture" :alt="`${firstName} ${lastName}`" :class="gender" />
  <h1>{{firstName}} {{lastName}}</h1>
  <h3>Email: {{email}}</h3>
  <button :class="gender" @click="getUser()">Next User</button>
</div> -->
<div id="app">
<div class="card mb-3">
  <img v-bind:src="picture" :alt="`${firstName} ${lastName}`" :class="gender" />
  <div class="card-body">
    <h5 class="card-title">{{firstName}} {{lastName}}</h5>
    <p class="card-text">Email: {{email}}</p>
    <p class="card-text"><small class="text-muted"> {{gender}}</small></p>
    <a :class="gender" @click="getUser()" class="btn btn-primary">Next</a>
  </div>
</div>

</div> 
</template>

<script>

// @ is an alias to /src
import 'bootstrap/dist/css/bootstrap.css'
// import axios from 'axios'
// import { info } from "vue";

export default {
   data(){
    return{
      firstName: 'John',
      lastName: 'Doe',
      email: 'john@gmail.com',
      gender: 'male',
      picture: 'https://randomuser.me/api/portraits/men/10.jpg',
    }
  },
  mounted() {
    this.load()
  },
  methods: {
   async getUser() {
      const res = await fetch('https://randomuser.me/api/')
      const { results } = await res.json()

      // console.log(results)

      this.firstName = results[0].name.first
      this.lastName = results[0].name.last
      this.email = results[0].email
      this.gender = results[0].gender
      this.picture = results[0].picture.large
    },
  
   }
  
  
}
</script>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html,
body {
  font-family: Arial, Helvetica, sans-serif;
}

#app {
  width: 400px;
  height: 100vh;
  margin: auto;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

h1,
h3 {
  margin-bottom: 1rem;
  font-weight: normal;
}


.male {
  border-color: steelblue;
  background-color: steelblue;
}

.female {
  border-color: pink;
  background-color: pink;
  color: #333;
}

button {
  cursor: pointer;
  display: inline-block;
  background: #333;
  color: white;
  font-size: 18px;
  border: 0;
  padding: 1rem 1.5rem;
}

button:focus {
  outline: none;
}

button:hover {
  transform: scale(0.98);
}

</style>