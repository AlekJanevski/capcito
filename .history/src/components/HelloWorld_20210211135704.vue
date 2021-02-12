<template>
		<!-- <table class="w-5/6 m-5 mx-auto text-gray-800 bg-gray-200 rounded-t-lg">
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
		</table> -->
		<div class="container px-4 mx-auto sm:px-8">
			<div class="py-8">
				<div>
					<h2 class="text-2xl font-semibold leading-tight">Companies</h2>
				</div>

				<div class="flex flex-col my-2 sm:flex-row">
					<div class="flex flex-row mb-1 sm:mb-0">
						<div class="relative mr-3">
							<select class="block w-full h-full px-4 py-2 pr-8 leading-tight text-gray-700 bg-white border border-gray-400 rounded-l appearance-none focus:outline-none focus:bg-white focus:border-gray-500">
								<option>5</option>
								<option>10</option>
								<option>20</option>
							</select>
							<div
								class="absolute inset-y-0 right-0 flex items-center px-2 text-gray-700 pointer-events-none">
								<svg class="w-4 h-4 fill-current" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
									<path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z" />
								</svg>
							</div>
						</div>
						<div class="relative mr-3">
							<select
								class="block w-full h-full px-4 py-2 pr-8 leading-tight text-gray-700 bg-white border border-gray-400 rounded appearance-none sm:rounded-r-none focus:outline-none focus:border-l focus:border-r focus:bg-white focus:border-gray-500">
								<option>All</option>
								<option>Active</option>
								<option>Inactive</option>
							</select>
							<div
								class="absolute inset-y-0 right-0 flex items-center px-2 text-gray-700 pointer-events-none">
								<svg class="w-4 h-4 fill-current" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
										<path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z" />
								</svg>
							</div>
						</div>
					</div>

					<div class="relative block">
						<span class="absolute inset-y-0 left-0 flex items-center h-full pl-2">
							<svg viewBox="0 0 24 24" class="w-4 h-4 text-gray-500 fill-current">
								<path d="M10 4a6 6 0 100 12 6 6 0 000-12zm-8 6a8 8 0 1114.32 4.906l5.387 5.387a1 1 0 01-1.414 1.414l-5.387-5.387A8 8 0 012 10z" />
							</svg>
						</span>

						    <input
									type="text"
									v-model.trim="search"
									placeholder="Search people..."
									@keyup="getAllStarWarsPeople"
								/>
						<input 
							type="text"
							v-model.trim="search"
							placeholder="Search companies by name"
							class="block w-full py-2 pl-8 pr-6 text-sm text-gray-700 placeholder-gray-400 bg-white border border-b border-gray-400 rounded-l rounded-r appearance-none sm:rounded-l-none focus:bg-white focus:placeholder-gray-600 focus:text-gray-700 focus:outline-none" />
					</div>
				</div>

				<div class="px-4 py-4 -mx-4 overflow-x-auto sm:-mx-8 sm:px-8">
					<div class="inline-block min-w-full overflow-hidden rounded-lg shadow">
						<table class="min-w-full leading-normal">
							<thead>
								<tr>
									<th class="px-5 py-3 text-xs font-semibold tracking-wider text-left text-gray-600 uppercase bg-gray-100 border-b-2 border-gray-200">
											Company id
									</th>
									<th class="px-5 py-3 text-xs font-semibold tracking-wider text-left text-gray-600 uppercase bg-gray-100 border-b-2 border-gray-200">
											Company name
									</th>
									<th class="px-5 py-3 text-xs font-semibold tracking-wider text-left text-gray-600 uppercase bg-gray-100 border-b-2 border-gray-200">
											Company type
									</th>
								</tr>
							</thead>

							<tbody>
									<tr v-for="user in usersList" :key="user.id">
										<td class="px-5 py-5 text-sm bg-white border-b border-gray-200">
											<div class="flex items-center">
												<p class="text-gray-900 whitespace-no-wrap">
													{{ user.id }}
												</p>
											</div>
										</td>

										<td class="px-5 py-5 text-sm bg-white border-b border-gray-200">
											<p class="text-gray-900 whitespace-no-wrap">
												{{ user.name }}
											</p>
										</td>

										<td class="px-5 py-5 text-sm bg-white border-b border-gray-200">
											<p class="text-gray-900 whitespace-no-wrap">
												{{ user.type }}
											</p>
										</td>
									</tr>
							</tbody>
						</table>
						<!-- <div
							class="flex flex-col items-center px-5 py-5 bg-white border-t xs:flex-row xs:justify-between ">
							<span class="text-xs text-gray-900 xs:text-sm">
								Showing 1 to 4 of 50 Entries
							</span>
							<div class="inline-flex mt-2 xs:mt-0">
								<button
									class="px-4 py-2 text-sm font-semibold text-gray-800 bg-gray-300 rounded-l hover:bg-gray-400">
									Prev
								</button>
								<button
									class="px-4 py-2 text-sm font-semibold text-gray-800 bg-gray-300 rounded-r hover:bg-gray-400">
									Next
								</button>
							</div>
						</div> -->
					</div>
				</div>
			</div>
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
