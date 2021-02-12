<template>
   <div>
		<h1> Companies listed </h1>
		<table class="rounded-t-lg m-5 w-5/6 mx-auto bg-gray-200 text-gray-800">
			<tr class="text-left border-b-2 border-gray-300">
				<th class="px-4 py-3">Company ID</th>
				<th class="px-4 py-3">Company name</th>
				<th class="px-4 py-3">Company type: </th>
			</tr>

			<tr class="bg-gray-100 border-b border-gray-200" v-for="user in usersList" :key="user.id">
				<td class="px-4 py-3">{{ user.id }}</td>
				<td class="px-4 py-3">{{ user.name }}</td>
				<td class="px-4 py-3">{{ user.type }}</td>
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
