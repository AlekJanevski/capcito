<template>
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
								<option 
									v-for="(type, index) in filterList"
									:key="index"
									@click="filter = type;"
								> {{ type }} </option>
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
							v-model="companyNameSearchString"
							placeholder="Search by name"
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
									<div v-for="(type, company) in companyFilteredFeed" :key="company.id">
										<tr>
											<td class="px-5 py-5 text-sm bg-white border-b border-gray-200">
												<div class="flex items-center">
													<p class="text-gray-900 whitespace-no-wrap">
														{{ company.id }}
													</p>
												</div>
											</td>

											<td class="px-5 py-5 text-sm bg-white border-b border-gray-200">
												<p class="text-gray-900 whitespace-no-wrap">
													{{ company.name }}
												</p>
											</td>

											<td class="px-5 py-5 text-sm bg-white border-b border-gray-200">
												<p class="text-gray-900 whitespace-no-wrap">
													{{ company.type }}
												</p>
											</td>
										</tr>
									</div>
							</tbody>
						</table>
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
      companyList: [],
			companyNameSearchString: '',
			fkey: "type",
			filterList: ["All", "AB", "HB", "EF"],
			filter: "All",
    };
  },

  mounted() {
		// Mounting the axios call to the api and fetching the data
    axios
			.get("https://my-json-server.typicode.com/capcito/frontend-ws/companies")
      .then(res => {
        this.companyList = res.data;
      })
      .catch(error => {
        console.log(error)
         // Manage errors if found any
      })
  },

	computed: {

		// Handles the filtered company feed when searched by name feed
		companyFilteredFeed: function () {

			var companies = this.companyList;
			var companyNameSearchString = this.companyNameSearchString;

			if (!companyNameSearchString){
				return companies;
			}

			companies = companies.filter(function(item){
				if (item.name.indexOf(companyNameSearchString) !== -1 || item.name.toLowerCase().indexOf(companyNameSearchString) !== -1){
					return item;
				}
			})

			return companies;
		}
	}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
