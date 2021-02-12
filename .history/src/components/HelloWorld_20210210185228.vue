<template>
  <div class="hello">
    <div v-for="company in companies.data" :key="company.id" ></div>
  </div>
</template>

<script>
import { toRefs, reactive, watch } from "@vue/composition-api";

export default {

  name: 'HelloWorld',

  function apiCall(url, options) {
    const state = reactive({
      response: [],
      error: null,
      fetching: true
    })

    const fetchData = async () => {
      try {
        const res = await fetch(url, options);
        const json = await res.json();
        state.response = json;
      } catch (errors) {
        state.error = errors;
      } finally {
        state.fetching = false;
      }
    };
    return { ...toRefs(state), fetchData };
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
