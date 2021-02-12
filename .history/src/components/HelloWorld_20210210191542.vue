<template>
  <div>
    <span> {{ results }}</span>
  </div>
</template>

<script>
import { useApi } from 'vue'

export default {
  name: 'Hello World',

  setup() {

    const userList =  useApi(()=>({url:`https://swapi.dev/api/people/1`}), (r)=> r.json());
    userList.execute(); // we can await for result
    // ...
    return {  ...userList }

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
