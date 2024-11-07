<script lang="ts">
	import { onMount } from 'svelte';
	import Header from '$lib/components/Header.svelte';
	import Papa from 'papaparse';

	import * as Table from '$lib/components/ui/table/index.js';

	import Card from '$lib/components/ui/card/card.svelte';
	import Input from '$lib/components/ui/input/input.svelte';
	import GdLogo from '$lib/components/icons/gd_logo.svelte';
	import Trophy from '$lib/components/icons/trophy.svelte';
	import Award from '$lib/components/icons/award.svelte';

	interface DataRow {
		'User Name': string;
		'User Email': string;
		'Google Cloud Skills Boost Profile URL': string;
		'Profile URL Status': string;
		'Access Code Redemption Status': string;
		'All Skill Badges & Games Completed': string;
		'# of Skill Badges Completed': number;
		'Names of Completed Skill Badges': string;
		'# of Arcade Games Completed': number;
		'Names of Completed Arcade Games': string;
	}

	let searchQuery: string = '';
	let data: DataRow[] = [];
	let filteredData: DataRow[] = [];

	onMount(async () => {
		const response = await fetch('/data.csv');
		const csvText = await response.text();
		Papa.parse<DataRow>(csvText, {
			header: true,
			complete: (results) => {
				data = results.data;
				filteredData = data;
			}
		});
	});

	function filterData() {
		filteredData = data.filter((item) =>
			item['User Name'].toLowerCase().includes(searchQuery.toLowerCase())
		);
	}
</script>

<div class="max-w-screen min-h-screen bg-gradient-to-br from-gray-900 to-gray-800">
	<Header />
	<div class="flex flex-col gap-8 p-4">
		<div class=" grid gap-4 md:grid-cols-2">
			<Card class="border-none bg-gradient-to-br from-gray-800 to-gray-900 p-6">
				<div class="flex items-center gap-4">
					<div class="rounded-lg bg-green-900 p-3">
						<Trophy class="h-6 w-6 text-green-400" />
					</div>
					<div>
						<p class="text-sm font-medium text-gray-400">Eligible Participants for swags</p>
						<p class="text-3xl font-bold text-gray-100">80</p>
					</div>
				</div>
			</Card>
			<Card class="border-none bg-gradient-to-br from-gray-800 to-gray-900 p-6">
				<div class="flex items-center gap-4">
					<div class="rounded-lg bg-blue-900 p-3">
						<Award class="h-6 w-6 text-blue-400" />
					</div>
					<div>
						<p class="text-sm font-medium text-gray-400">Total Participants</p>
						<p class="text-3xl font-bold text-gray-100">{data.length}</p>
					</div>
				</div>
			</Card>
		</div>
		<div class="relative">
			<Input
				type="text"
				placeholder="Search participants by name..."
				bind:value={searchQuery}
				on:input={filterData}
				class="rounded-lg border-none bg-gray-800 pl-10 text-gray-100 placeholder-gray-500 focus:border-none"
			/>
		</div>

		<Card
			class="overflow-hidden rounded-lg border-none bg-gradient-to-br from-gray-800 to-gray-900"
		>
			<Table.Root class=" border-slate-300 text-gray-200">
				<Table.Header>
					<Table.Row class="border-gray-500 ">
						<Table.Head class="text-center text-gray-100">Name</Table.Head>
						<Table.Head class="text-center text-gray-100">Redemption Status</Table.Head>
						<Table.Head class="text-center text-gray-100"
							>No. of All Skill Badges & Games Completed</Table.Head
						>
						<Table.Head class="text-center text-gray-100">No. of Skill Badges Completed</Table.Head>
						<Table.Head class="text-center text-gray-100">No. of Arcade Games Completed</Table.Head>
						<Table.Head class="text-center text-gray-100"
							>Names of Completed Arcade Games</Table.Head
						>
					</Table.Row>
				</Table.Header>
				<Table.Body>
					{#each filteredData as row}
						<Table.Row class=" border-gray-500 disabled:pointer-events-none">
							<Table.Cell>{row['User Name']}</Table.Cell>
							<Table.Cell>{row['Access Code Redemption Status']}</Table.Cell>
							<Table.Cell>{row['All Skill Badges & Games Completed']}</Table.Cell>
							<Table.Cell>{row['# of Skill Badges Completed']}</Table.Cell>
							<Table.Cell>{row['# of Arcade Games Completed']}</Table.Cell>
							<Table.Cell>{row['Names of Completed Arcade Games']} ss</Table.Cell>
						</Table.Row>
					{/each}
				</Table.Body>
			</Table.Root>
		</Card>
	</div>
</div>

<style>
</style>
