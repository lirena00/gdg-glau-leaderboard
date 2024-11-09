<script lang="ts">
	import * as Table from '$lib/components/ui/table/index.js';
	import Card from '$lib/components/ui/card/card.svelte';

	interface Lab {
		name: string;
		url: string;
	}

	const labs: Lab[] = [
		{
			name: 'The Basics of Google Cloud Compute',
			url: 'https://www.cloudskillsboost.google/course_templates/754?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Get Started with Cloud Storage',
			url: 'https://www.cloudskillsboost.google/course_templates/725?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Get Started with Pub/Sub',
			url: 'https://www.cloudskillsboost.google/course_templates/728?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Get Started with API Gateway',
			url: 'https://www.cloudskillsboost.google/course_templates/662?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Get Started with Looker',
			url: 'https://www.cloudskillsboost.google/course_templates/647?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Get Started with Dataplex',
			url: 'https://www.cloudskillsboost.google/course_templates/726?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Get Started with Google Workspace Tools',
			url: 'https://www.cloudskillsboost.google/course_templates/676?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Cloud Functions: 3 Ways',
			url: 'https://www.cloudskillsboost.google/course_templates/696?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'App Engine: 3 Ways',
			url: 'https://www.cloudskillsboost.google/course_templates/671?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Cloud Speech API: 3 Ways',
			url: 'https://www.cloudskillsboost.google/course_templates/700?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Monitoring in Google Cloud',
			url: 'https://www.cloudskillsboost.google/course_templates/747?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Networking Fundamentals on Google Cloud',
			url: 'https://www.cloudskillsboost.google/course_templates/748?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Analyze Images with the Cloud Vision API',
			url: 'https://www.cloudskillsboost.google/course_templates/633'
		},
		{
			name: 'Prompt Design in Vertex AI',
			url: 'https://www.cloudskillsboost.google/course_templates/976?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		},
		{
			name: 'Develop GenAI Apps with Gemini and Streamlit',
			url: 'https://www.cloudskillsboost.google/course_templates/978'
		},
		{
			name: 'Diwali in the Arcade [Access Code: 1q-diwali-1111]',
			url: 'https://www.cloudskillsboost.google/games/5628?utm_source=gcaf-site&utm_medium=website&utm_campaign=arcade-facilitator24'
		}
	];
</script>

<Card
	class="w-full overflow-hidden rounded-lg border-none bg-gradient-to-br from-gray-800 to-gray-900 md:w-3/4"
>
	<Table.Root class=" border-slate-300 text-gray-200">
		<Table.Header>
			<Table.Row class="border-gray-500 ">
				<Table.Head class="text-center text-gray-100">Study Jams Syllabus</Table.Head>
			</Table.Row>
		</Table.Header>
		<Table.Body>
			{#each labs as lab}
				<Table.Row class="border-gray-500 ">
					<Table.Cell
						><a class="text-[#63b3ed] hover:underline" href={lab.url} target="_blank">{lab.name}</a
						></Table.Cell
					>
				</Table.Row>
			{/each}
		</Table.Body>
	</Table.Root>
</Card>
