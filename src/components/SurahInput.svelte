<script>
	import { createEventDispatcher } from 'svelte';
	let searchQuery = '';
	const dispatch = createEventDispatcher();

	function handleInput() {
		console.log('Search query:', searchQuery);
		dispatch('search', { query: searchQuery });
	}
</script>

<main class="hero font-serif my-10">
	<div class="hero-content text-center">
		<div class="join">
			<input
				type="text"
				class="join-item input input-bordered max-w-xs"
				placeholder="Search a Surah"
				bind:value={searchQuery}
				on:input={handleInput}
			/>
			<button type="button" class="join-item btn btn-primary rounded-r-full" on:click={handleInput}
				><i class="ri-search-line"></i>Search</button
			>
		</div>
	</div>
</main>
<div class="divider mx-10">Surahs</div>
<!-- <i class="ri-search-line"></i> -->
