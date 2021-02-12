<template>
   <div>
    <ul class="test-list">
      <li v-for="user in usersList" :key="user.id">
        <span>Company ID: {{ user.id }}</span>
        <span>Company name: {{ user.name }}</span>
        <span>Company type: {{ user.type }}</span>
      </li>
    </ul>

		<table class="rounded-t-lg m-5 w-5/6 mx-auto bg-gray-200 text-gray-800">
			<tr class="text-left border-b-2 border-gray-300">
				<th class="px-4 py-3">Firstname</th>
				<th class="px-4 py-3">Lastname</th>
				<th class="px-4 py-3">Age</th>
				<th class="px-4 py-3">Sex</th>
			</tr>
		</table>
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

</style>
