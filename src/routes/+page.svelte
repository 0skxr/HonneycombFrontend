<script>
	import Chat from './Chat.svelte';
	import Message from './message.svelte';

	let items = [
		{ content: 'I am red!', component: Message },
		{ content: 'I am blue!', component: Message }
	];
</script>

<Chat />

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.gray.100);
	}
</style>
