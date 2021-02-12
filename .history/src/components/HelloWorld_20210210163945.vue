<template>
  <div class="hello">
    <div v-for="user in users.data" :key="user.id" ></div>
  </div>
</template>

<script>
import { ref } from "vue"

export default {
  name: 'HelloWorld',

  async setup() {
    const users = ref(null);
    const response = await fetch("https://regres.in/api/users?delay=2")
    users.value = await response.json();

    return { users }

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
