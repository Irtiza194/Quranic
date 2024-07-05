<script>
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	export let searchQuery = '';
	let surahs = [];
	let filteredSurahs = [];
	let loading = false;

	onMount(async () => {
		try {
			const response = await fetch('https://api.quran.com/api/v4/chapters');
			const data = await response.json();
			surahs = data.chapters;
			filterSurahs();
		} catch (error) {
			console.error('Error fetching surah data:', error);
		}
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

	function navigateToSurah(surah) {
		goto(`/surah/${surah.id}`);
	}
</script>

<section class="overflow-hidden mt-5 mb-5">
	<div
		id="surahList"
		class="px-10 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4"
	>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		{#each filteredSurahs as surah}
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<!-- svelte-ignore a11y-no-static-element-interactions -->
			<div
				class="p-4 border text-center hover:bg-base-100 hover:shadow-lg duration-300 cursor-pointer"
				on:click={() => navigateToSurah(surah)}
			>
				<h2 class="text-lg text-center max-md:text-base max-sm:text-sm">
					{surah.name_simple}
				</h2>
				<h3 class="text-lg surahFont text-gray-600 max-md:text-base max-sm:text-sm">
					{surah.name_arabic}
				</h3>
			</div>
		{/each}
	</div>
</section>
