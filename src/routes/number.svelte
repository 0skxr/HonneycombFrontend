<script>
	let name = '';
	let data = '';

	async function getGreeting() {
		try {
			const endpoint = 'http://127.0.0.1:5000/hello?name=' + name;
			const response = await fetch(endpoint);
			if (!response.ok) {
				// Handle HTTP errors
				throw new Error('Network response was not ok');
			}
			data = await response.text(); // or response.json() if the server responds with JSON
			console.log(data);
		} catch (error) {
			console.error('There was a problem with your fetch operation:', error);
		}
	}
</script>

<form on:submit|preventDefault={getGreeting}>
	<input type="text" bind:value={name} placeholder="Gib deinen Namen ein" />
	<button type="submit">Begrüße mich</button>
</form>

<h1>{data}</h1>
