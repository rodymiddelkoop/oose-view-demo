<template>
  <div id="hello">
    <img src="http://vuejs.org/images/logo.png">

    <h1>{{ msg }}</h1>
    <div v-for="linkGroup of linkGroups">
    <h2>{{linkGroup.name}}</h2>
    <ul>
      <li v-for="link of linkGroup.links"><a :href="link.url"> {{ link.text }} </a></li>
    </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
const config = {
    method: 'get',
    url: "http://localhost:8080/db.json"
  };

export default {
  name: 'hello',
  data () {
    return {
      msg: '',
      linkGroups: []
    }
  },

  created() {
    axios.request(config)
    .then(response => {
      // JSON responses are automatically parsed.
      this.linkGroups = response.data
      this.msg = "Done!"
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>

<style scoped>
#hello {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
