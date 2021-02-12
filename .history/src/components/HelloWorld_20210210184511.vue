<template>
  <div class="hello">
    <div v-for="company in companies.data" :key="company.id" ></div>
  </div>
</template>

<script>
import { ref } from "vue"

export default {
  name: 'HelloWorld',

  async setup() {
    const companies = ref(null);
    const response = await fetch("https://my-json-server.typicode.com/capcito/frontend-ws/companies");
    companies.value = await response.json();

    return { companies }

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
