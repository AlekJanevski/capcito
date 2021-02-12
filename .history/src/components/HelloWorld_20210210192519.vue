<template>
   <div>
    <ul class="test-list">
      <li v-for="user in usersList" :key="user.id">
        <span>Company ID: {{ user.id }}</span>
        <span>Company name: {{ user.name }}</span>
        <span>Company type: {{ user.type }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Hello World',

  data() {
    return {
      usersList: []
    };
  },

  mounted() {
    axios.get("https://my-json-server.typicode.com/capcito/frontend-ws/companies")
      .then(res => {
        this.usersList = res.data;
        console.log(this.usersList)
      })
      .catch(error => {
        console.log(error)
         // Manage errors if found any
      })
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
