<script>
	import { onMount } from 'svelte';

	export let searchQuery = '';
	let surahs = [];
	let filteredSurahs = [];
	let verses = [];
	let selectedSurah = null;

	onMount(async () => {
		try {
			const response = await fetch('https://api.quran.com/api/v4/chapters');
			if (!response.ok) {
				throw new Error('Failed to fetch Surahs. Please try again later.');
			}
			const data = await response.json();
			surahs = data.chapters;
			filterSurahs();
		} catch (error) {
			console.error('Error fetching surah data:', error.message);
			// You can handle the error here, e.g., display an error message to the user
		}
	});

	// Filter Surahs based on search query
	function filterSurahs() {
		if (!searchQuery) {
			filteredSurahs = surahs;
		} else {
			const query = searchQuery.toLowerCase();
			filteredSurahs = surahs.filter((surah) => surah.name_simple.toLowerCase().includes(query));
		}
	}

	// Fetch verses for the selected Surah
	async function fetchVerses(surah) {
		try {
			const response = await fetch(
				`https://api.alquran.cloud/v1/surah/${surah.id}/editions/quran-uthmani,en.sahih`
			);
			if (!response.ok) {
				throw new Error('Failed to fetch verses. Please try again later.');
			}
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
			console.error('Error fetching verses:', error.message);
			// You can handle the error here, e.g., display an error message to the user
		}
	}

	// Go back to Surah list
	function goBack() {
		selectedSurah = null;
		verses = [];
		// Scroll to the Surah list
		document.getElementById('surahList').scrollIntoView({ behavior: 'smooth' });
	}
</script>

<section class="hero">
	{#if !selectedSurah}
		<div id="surahList" class="hero-content grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4">
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<!-- svelte-ignore a11y-no-static-element-interactions -->
			{#each filteredSurahs as surah}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<div
					class="card shadow-lg p-4 border-[1px] border-neutral-900 hover:bg-base-200 duration-300 cursor-pointer"
					on:click={() => fetchVerses(surah)}
				>
					<h2 class="text-lg surahFont max-md:text-base max-sm:text-sm">
						<i class="ri-book-marked-line mr-2"></i>{surah.name_simple}
					</h2>
				</div>
			{/each}
		</div>
	{:else}
		<div class="mt-8">
			<button class="btn btn-primary mb-4 floating-button" on:click={goBack}>
				<i class="ri-arrow-go-back-line mr-2"></i>Go Back
			</button>
			<h3 class="text-2xl font-bold mb-4 px-20 surahFont">
				{selectedSurah.name_simple} (Chapter {selectedSurah.id})
			</h3>
			<ul class="list-decimal ml-4 px-20">
				{#each verses as verse}
					<li class="mb-2">
						<p class="text-lg">{verse.arabic}</p>
						<p class="text-md text-gray-600">{verse.english}</p>
					</li>
				{/each}
			</ul>
		</div>
	{/if}
</section>
