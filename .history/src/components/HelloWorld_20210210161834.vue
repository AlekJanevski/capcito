<template>
  <div class="hello">
    <ul v-if="!loading && data && data.length">
      <li v-for="(index, post) of data" :key="index">
        <p><strong> {{ post }}</strong></p>
        <p></p>
      </li>
    </ul>

    <p v-if="loading">
      Still loading..
    </p>
    <p v-if="error">
      There is an error
    </p>
  </div>
</template>

<script>
import { ref } from "vue";
import { onMounted } from 'vue'

export default {
  name: 'HelloWorld',

  setup() {
    const data = ref(null);
    const loading = ref(true);
    const error = ref(null);

    function fetchData() {
      loading.value = true;
      // I prefer to use fetch
      // you can use use axios as an alternative
      return fetch('http://jsonplaceholder.typicode.com/posts', {
        method: 'get',
        headers: {
          'content-type': 'application/json'
        }
      })
      .then(res => {
        // a non-200 response code
        if (!res.ok) {
          // create error instance with HTTP status text
          const error = new Error(res.statusText);
          error.json = res.json();
          throw error;
        }

        return res.json();
      })
      .then(json => {
        // set the response data
        data.value = json.data;
      })
      .catch(err => {
        error.value = err;
        // In case a custom JSON error response was provided
        if (err.json) {
          return err.json.then(json => {
            // set the JSON response message
            error.value.message = json.message;
          });
        }
      })
      .then(() => {
        loading.value = false;
      });
    }

    onMounted(() => {
      fetchData();
    });

    return {
      data,
      loading,
      error
    };
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
