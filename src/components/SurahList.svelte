<script>
	import { onMount } from 'svelte';

	export let searchQuery = '';
	let surahs = [];
	let filteredSurahs = [];
	let verses = [];
	let selectedSurah = null;
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

	async function fetchVerses(surah) {
		try {
			loading = true;
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
			loading = false;
		} catch (error) {
			console.error('Error fetching verses:', error);
			loading = false;
		}
	}

	function goBack() {
		selectedSurah = null;
		verses = [];
		document.getElementById('surahList').scrollIntoView({ behavior: 'smooth' });
	}
</script>

<section class="hero overflow-hidden">
	{#if !selectedSurah}
		<div id="surahList" class="hero-content grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4">
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			{#each filteredSurahs as surah}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div
					class="p-4 border-[1px] text-center border-neutral-400 hover:bg-base-100 hover:shadow-lg duration-300 cursor-pointer"
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
			<div class="fixed top-0 left-0 right-0 bg-base-300 py-4 z-10 shadow-md">
				<h3 class="text-2xl font-bold mb-2 px-20 surahFont max-sm:px-5">
					{selectedSurah.name_simple} (Chapter {selectedSurah.id})
				</h3>
				<h4 class="text-xl font-bold px-20 surahFont text-gray-600 max-sm:px-5">
					{selectedSurah.name_arabic}
				</h4>
			</div>
			<div class="mt-24 h-[calc(100vh-6rem)] overflow-auto px-20 max-sm:px-5 surah-container">
				<ul class="list-decimal ml-4">
					{#each verses as verse}
						<li class="mb-2">
							<p class="text-2xl text-right arabicFont">{verse.arabic}</p>
							<p class="mb-10 mt-9">{verse.english}</p>
							<div class="divider"></div>
						</li>
					{/each}
				</ul>
			</div>
		</div>
	{/if}
</section>
