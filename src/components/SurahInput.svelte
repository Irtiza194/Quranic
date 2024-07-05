<script>
	import Input from '$lib/components/ui/input/input.svelte';
	import { createEventDispatcher } from 'svelte';
	let searchQuery = '';
	const dispatch = createEventDispatcher();

	function handleInput() {
		console.log('Search query:', searchQuery);
		dispatch('search', { query: searchQuery });
	}
</script>

<main class="font-serif border-b p-10">
	<div class="flex justify-center items-center">
		<Input
			type="text"
			class="max-w-xs text-center"
			placeholder="Search a Surah"
			bind:value={searchQuery}
			on:input={handleInput}
		></Input>
	</div>
</main>
