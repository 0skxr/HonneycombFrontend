<script>
	import { marked } from 'marked';
	export let content = '';
	export let sender = '';
	export let imageLink = '';
</script>

<div class="flex"></div>

<div class="flex-none flex flex-row space-x-4">
	<div class="flex-none box-border h-6 w-6">
		<div class="flex-none rounded-full">
			<img src={imageLink} class="rounded-full" />
		</div>
	</div>
	<div class="flex flex-col ...">
		<h1 class="font-bold">{sender}</h1>
		<div>{@html marked(content)}</div>
	</div>
</div>
