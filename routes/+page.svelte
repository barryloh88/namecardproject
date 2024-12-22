<script>
	import { Alert } from 'flowbite-svelte';

	let clientIp = null;
	let error = null;

	// Fetch data from the API route when the component loads
	const fetchClientIp = async () => {
		try {
			const response = await fetch('/api/getIPaddress');
			if (!response.ok) {
				throw new Error('Failed to fetch client IP');
			}
			const data = await response.json();
			clientIp = data.clientIp;
		} catch (err) {
			error = err.message;
		}
	};

	fetchClientIp();
</script>

{#if error}
	<p>Error: {error}</p>
{:else if clientIp}
	<p>Your IP Address: {clientIp}</p>
{:else}
	<p>Loading...</p>
{/if}

<h1 class="text-3xl font-bold underline">Welcome to SvelteKit</h1>

<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>
<p>Welcome to Sveltekit!</p>
<button class="rounded bg-blue-500 px-6 py-2 font-bold text-white hover:bg-blue-600">
	Click Me
</button>

<button class="rounded bg-blue-500 px-4 py-2 font-bold text-white hover:bg-blue-700">
	Flowbite Button
</button>

<div class="p-8">
	<Alert>
		<span class="font-medium">Info alert!</span>
		Change a few things up and try submitting again.
	</Alert>
</div>

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.gray.100);
	}
</style>
