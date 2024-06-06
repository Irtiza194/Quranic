<script>
	import { onMount } from 'svelte';
	export let searchQuery = '';
	let surahs = [];
	let filteredSurahs = [];

	onMount(async () => {
		const response = await fetch('https://api.quran.com/api/v4/chapters');
		const data = await response.json();
		surahs = data.chapters;
		filterSurahs();
	});

	$: {
		console.log('Received search query in SurahList:', searchQuery);
		filterSurahs();
	}

	function filterSurahs() {
		if (searchQuery) {
			filteredSurahs = surahs.filter((surah) =>
				surah.name_simple.toLowerCase().includes(searchQuery.toLowerCase())
			);
		} else {
			filteredSurahs = surahs;
		}
		console.log('Filtered Surahs in SurahList:', filteredSurahs);
	}
</script>

<section class="hero">
	<div class="hero-content grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
		{#each filteredSurahs as surah}
			<div class="card bordered shadow-lg p-4">
				<h2 class="text-xl font-bold">
					<i class="ri-book-marked-line mr-2"></i>{surah.name_simple}
				</h2>
			</div>
		{/each}
	</div>
</section>
