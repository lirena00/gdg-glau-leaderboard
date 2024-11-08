<script lang="ts">
	import { onMount } from 'svelte';
	import Header from '$lib/components/Header.svelte';
	import LabsTable from '$lib/components/LabsTable.svelte';
	import Footer from '$lib/components/Footer.svelte';

	import Papa from 'papaparse';

	import * as Table from '$lib/components/ui/table/index.js';

	import Card from '$lib/components/ui/card/card.svelte';
	import Input from '$lib/components/ui/input/input.svelte';
	import Search from '$lib/components/icons/search.svelte';
	import Trophy from '$lib/components/icons/trophy.svelte';
	import Award from '$lib/components/icons/award.svelte';

	interface DataRow {
		'User Name': string;
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

<svelte:head>
	<title>GDG GLAU Leaderboard</title>
</svelte:head>

<div class="max-w-screen dark min-h-screen bg-gradient-to-br from-gray-900 to-gray-800">
	<Header />
	<div class="flex flex-col items-center justify-center gap-8 p-4">
		<div class=" grid w-full justify-center gap-4 md:w-3/4 md:grid-cols-2">
			<Card class="border-none bg-gradient-to-br from-gray-800 to-gray-900 p-6">
				<div class="flex items-center gap-4">
					<div class="rounded-lg bg-green-900 p-3">
						<Trophy class="h-6 w-6 text-green-400" />
					</div>
					<div>
						<p class="text-sm font-medium text-gray-400">Eligible Participants for swags</p>
						<p class="text-3xl font-bold text-gray-100">
							{data.filter((row) => row['All Skill Badges & Games Completed'] == 'Yes').length}
						</p>
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
		<div class="relative w-full md:w-3/4">
			<Search class="absolute left-3 top-1/2 h-4 w-4 -translate-y-1/2 text-muted-foreground " />
			<Input
				type="text"
				placeholder="Search participants by name..."
				bind:value={searchQuery}
				on:input={filterData}
				class="rounded-lg border-none bg-gray-800 pl-10 text-gray-100 placeholder-gray-500 focus-visible:ring-offset-1"
			/>
		</div>

		<Card
			class="w-full overflow-hidden rounded-lg border-none bg-gradient-to-br from-gray-800 to-gray-900 md:w-3/4"
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
					</Table.Row>
				</Table.Header>
				<Table.Body>
					{#each filteredData.sort((a, b) => b['# of Skill Badges Completed'] - a['# of Skill Badges Completed']) as row}
						<Table.Row class="border-gray-500 disabled:pointer-events-none ">
							<Table.Cell
								><a href={row['Google Cloud Skills Boost Profile URL']} target="_blank"
									>{row['User Name']}</a
								>
								{#if row['All Skill Badges & Games Completed'] == 'Yes'}
									<Trophy class="ml-1 inline-block h-4 w-4 text-yellow-500" />
								{/if}
							</Table.Cell>
							<Table.Cell>{row['Access Code Redemption Status']}</Table.Cell>
							<Table.Cell>{row['All Skill Badges & Games Completed']}</Table.Cell>
							<Table.Cell>{row['# of Skill Badges Completed']}</Table.Cell>
							<Table.Cell>{row['# of Arcade Games Completed']}</Table.Cell>
						</Table.Row>
					{/each}
				</Table.Body>
			</Table.Root>
		</Card>
		<LabsTable />
	</div>
	<Footer />
</div>

<style>
</style>
