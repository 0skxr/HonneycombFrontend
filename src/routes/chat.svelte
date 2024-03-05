<script>
	import { onMount } from 'svelte';
	import List from './List.svelte';
	import Message from './Message.svelte';
	import SvelteMarkdown from 'svelte-markdown';
	import { json } from '@sveltejs/kit';

	let items = [{}];
	let customText = '';

	/**
	 * @param {string} customText
	 */
	async function fetchData(customText) {
		const response = await fetch('http://127.0.0.1:5000/invoke?promt=' + customText);
		if (response.ok) {
			const data = await response.json();
			return data;
		} else {
			console.error('Failed to fetch data:', response.statusText);
			return null;
		}
	}

	/**
	 * @param {string} customText
	 */
	async function addItemToChat(customText) {
		items = [
			...items,
			{
				content: customText,
				sender: 'Du',
				imageLink: 'https://i.pinimg.com/originals/bd/b6/52/bdb6529e0356aaed61782636142d37c2.jpg',
				component: Message
			}
		];
		const data = await fetchData(customText);
		let content = data['content'];
		if (data) {
			items = [
				...items,
				{
					content: content,
					sender: 'LLM',
					imageLink:
						'https://djeqr6to3dedg.cloudfront.net/repo-logos/ollama/ollama/live/logo-1701412810306.png',
					component: Message
				}
			];
		}
	}
</script>

<div class="flex flex-row">
	<div class="basis-1/4"></div>
	<div class="flex-initial basis-2/4 flex flex-col space-y-4">
		<List {items} />
	</div>
	<div class="basis-1/4"></div>
</div>

<div class="fixed bottom-20 w-full">
	<div class="flex flex-row justify-center items-center">
		<div class="flex-grow"></div>
		<form on:submit={() => addItemToChat(customText)} class="w-1/2">
			<input
				type="text"
				class="w-full border-2 border-black px-4 py-3 leading-9 rounded-xl"
				bind:value={customText}
				placeholder="Prompt"
			/>
		</form>
		<div class="flex-grow"></div>
	</div>
</div>
