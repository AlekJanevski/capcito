<template>
	<div class="container px-4 mx-auto sm:px-8">
		<div class="py-8">
			<!-- Heading starts-->
			<div>
				<h2 class="mb-5 text-2xl font-semibold leading-tight">Companies table</h2>
			</div>
			<!-- Heading ends -->

			<!-- Filter section starts -->
			<div class="flex flex-col items-start justify-start my-2">
				<!-- Buttons wrapper starts -->
				<div class="flex items-center justify-start">
					<span class="inline-block"> Sort by: </span>
					<button
						@click="sortByAscending()"
						type="button"
						class="px-4 py-2 m-2 text-white transition duration-500 bg-indigo-500 border border-indigo-500 rounded-md select-none ease hover:bg-indigo-600 focus:outline-none focus:shadow-outline"
					>
						Ascending
					</button>
					<button
						@click="sortByDescending()"
						type="button"
						class="px-4 py-2 m-2 text-white transition duration-500 bg-indigo-500 border border-indigo-500 rounded-md select-none ease hover:bg-indigo-600 focus:outline-none focus:shadow-outline"
					>
						Descending
					</button>
				</div>
				<!-- Buttons wrapper ends -->

				<!-- Sorting filters wrapper starts -->
				<div class="relative flex flex-row w-full mb-1 sm:mb-0">
					<span class="flex items-center justify-start mr-3"> Filter by type: </span>
					<div class="relative mr-3">
						<select @change="handleFilterByType($event)"
							class="block w-full h-full px-4 py-2 pr-8 leading-tight text-gray-700 bg-white border border-gray-400 rounded appearance-none sm:rounded-r-none focus:outline-none focus:border-l focus:border-r focus:bg-white focus:border-gray-500">
							<option 
								v-for="(type, index) in filterList"
								:key="index"
								:value="type"
							> {{ type }} </option>
						</select>
						<div
							class="absolute inset-y-0 right-0 flex items-center px-2 text-gray-700 pointer-events-none">
							<svg class="w-4 h-4 fill-current" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
								<path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z" />
							</svg>
						</div>
					</div>

					<!-- Search field wrapper starts -->
					<div class="absolute right-0">
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
					<!-- Search field wrapper ends -->
				</div>
				<!-- Sorting filters wrapper ends -->
			</div>
			<!-- Filters section ends -->

			<!-- Table wrapper starts -->
			<div class="px-4 py-4 -mx-4 overflow-x-auto sm:-mx-8 sm:px-8">
				<div class="inline-block min-w-full overflow-hidden rounded-lg shadow">
					<table class="min-w-full leading-normal">
						<!-- Table header starts -->
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
						<!-- Table header ends -->
						
						<!-- Table body starts -->
						<tbody>
							<tr v-for="company in companyFilteredFeed.slice().reverse()" :key="company.id">
								<template v-if="company[fkey] === filter || filter === 'All'">
									<!-- Company id -->
									<td class="px-5 py-5 text-sm bg-white border-b border-gray-200">
										<div class="flex items-center">
											<p class="text-gray-900 whitespace-no-wrap">
												{{ company.id }}
											</p>
										</div>
									</td>
									<!-- Company name -->
									<td class="px-5 py-5 text-sm bg-white border-b border-gray-200">
										<p class="text-gray-900 whitespace-no-wrap">
											{{ company.name }}
										</p>
									</td>
									<!-- Company type -->
									<td class="px-5 py-5 text-sm bg-white border-b border-gray-200">
										<p class="text-gray-900 whitespace-no-wrap">
											{{ company.type }}
										</p>
									</td>
								</template>
							</tr>
						</tbody>
						<!-- Table body ends -->
					</table>
				</div>
			</div>
			<!-- Table wrapper ends -->
		</div>
	</div>
</template>

<script>
import axios from 'axios';
import { ref, onMounted, computed } from 'vue'

export default {
  name: 'Hello World',

	setup () {
		// Declaring data
		const companyList = ref([])
		const filter = ref("All")
		const companyNameSearchString = ref("")
		const fkey = ref("type")
		const filterList = ref(["All", "AB", "HB", "EF"])

		// Mounted
    onMounted(() => {
			axios
				.get("https://my-json-server.typicode.com/capcito/frontend-ws/companies")
				.then(res => {
					companyList.value = res.data;
				})
				.catch(error => {
					console.log(error)
					// Manage errors if found any
				})
			})

			// Methods
			// Handle the company filtering by company type
			function handleFilterByType (event) {
				filter.value = event.target.value
			}

			function sortByDescending () {
				companyFilteredFeed.value.sort((a, b) => { return a.id - b.id; })
			}

			function sortByAscending () {
				companyFilteredFeed.value.sort((a, b) => { return b.id - a.id; })
			}

			// Computed
			const companyFilteredFeed = computed(() => {
				const companies = companyList.value;

				if (!companyNameSearchString.value) {
					return companies;
				}

				return companies.filter(function(item) {
					if (item.name.indexOf(companyNameSearchString.value) !== -1 || item.name.toLowerCase().indexOf(companyNameSearchString.value) !== -1){
						return item;
					}
				})
			})

			// Return data
			return {
				companyList,
				handleFilterByType,
				filter,
				companyFilteredFeed,
				companyNameSearchString,
				fkey,
				filterList,
				sortByDescending,
				sortByAscending
			}
	}
}

</script>
