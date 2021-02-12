<template>
  <div>
    <ul v-if="!loading && data && data.length">
      <li v-for="post of data" :key="post">
        <p><strong>{{ post.title }}</strong></p>
        <p></p>
      </li>
    </ul>

    <p v-if="loading">
    Still loading..
    </p>
    <p v-if="error">


    </p>
  </div>
</template>

<script>
import { onMounted } from 'vue'
import axios from 'axios'

export default {
  name: 'Hello World',

  setup() {

    onMounted(() => {
      axios.get("https://my-json-server.typicode.com/capcito/frontend-ws/companies")
      .then(response => {this.results = response.data.results})
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
