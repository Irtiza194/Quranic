<script>
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import * as Card from '$lib/components/ui/card';

	export let searchQuery = '';
	let surahs = [];
	let filteredSurahs = [];

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
		class="mx-10 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4"
	>
		{#each filteredSurahs as surah}
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<!-- svelte-ignore a11y-no-static-element-interactions -->
			<div on:click={() => navigateToSurah(surah)} class="">
				<Card.Root
					class="hover:bg-neutral-300 dark:hover:bg-slate-900 hover:shadow-lg duration-300 cursor-pointer"
				>
					<Card.Header class="flex justify-around items-center flex-row">
						<Card.Title>{surah.name_simple}</Card.Title>
						<p class="arabicFont">{surah.name_arabic}</p>
					</Card.Header>
				</Card.Root>
			</div>
		{/each}
	</div>
</section>
