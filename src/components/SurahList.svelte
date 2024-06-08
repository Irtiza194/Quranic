<script>
	import { onMount } from 'svelte';
	import { afterUpdate } from 'svelte';

	export let searchQuery = '';
	let surahs = [];
	let filteredSurahs = [];
	let verses = [];
	let selectedSurah = null;

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

	async function fetchVerses(surah) {
		try {
			const response = await fetch(
				`https://api.alquran.cloud/v1/surah/${surah.id}/editions/quran-uthmani,en.sahih`
			);
			const data = await response.json();
			const arabicVerses = data.data[0].ayahs;
			const englishVerses = data.data[1].ayahs;

			// Combine Arabic and English verses into a single array
			verses = arabicVerses.map((arabicVerse, index) => ({
				number: arabicVerse.numberInSurah,
				arabic: arabicVerse.text,
				english: englishVerses[index].text
			}));

			selectedSurah = surah;
		} catch (error) {
			console.error('Error fetching verses:', error);
		}
	}

	function goBack() {
		selectedSurah = null;
		verses = [];
	}
</script>

<section class="hero">
	{#if !selectedSurah}
		<div class="hero-content grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4">
			{#each filteredSurahs as surah}
				<div
					class="p-4 border-[1px] text-center border-neutral-400 rounded hover:bg-base-100 hover:shadow-lg duration-300 cursor-pointer"
					on:click={() => fetchVerses(surah)}
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
	{:else}
		<div class="mt-8">
			<button class="btn btn-error mb-4 floating-button" on:click={goBack}>
				<i class="ri-arrow-go-back-line mr-2"></i>Go Back
			</button>
			<h3 class="text-2xl font-bold mb-4 px-20 surahFont max-sm:px-5">
				{selectedSurah.name_simple} (Chapter {selectedSurah.id})
			</h3>
			<h4 class="text-xl font-bold mb-4 px-20 surahFont text-gray-600 max-sm:px-5">
				{selectedSurah.name_arabic}
			</h4>
			<ul class="list-decimal ml-4 px-20 max-sm:px-5">
				{#each verses as verse}
					<li class="mb-2">
						<p class="text-lg surahFont">{verse.arabic}</p>
						<p class="text-md">{verse.english}</p>
					</li>
					{#if verse.number !== verses[verses.length - 1].number}
						<div class="divider"></div>
					{/if}
				{/each}
			</ul>
		</div>
	{/if}
</section>
