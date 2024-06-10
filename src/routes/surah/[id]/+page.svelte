<script>
	import { onMount } from 'svelte';
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';

	let surahId;
	let surah = null;
	let verses = [];
	let loading = false;

	// Extract surahId from the page URL
	$: surahId = $page.params.id;

	onMount(async () => {
		try {
			const response = await fetch(`https://api.quran.com/api/v4/chapters/${surahId}`);
			const data = await response.json();
			surah = data.chapter;
			await fetchVerses(surahId);
		} catch (error) {
			console.error('Error fetching surah data:', error);
		}
	});

	async function fetchVerses(id) {
		try {
			loading = true;
			const response = await fetch(
				`https://api.alquran.cloud/v1/surah/${id}/editions/quran-uthmani,en.sahih`
			);
			const data = await response.json();
			const arabicVerses = data.data[0].ayahs;
			const englishVerses = data.data[1].ayahs;

			verses = arabicVerses.map((arabicVerse, index) => ({
				number: arabicVerse.numberInSurah,
				arabic: arabicVerse.text,
				english: englishVerses[index].text
			}));
			loading = false;
		} catch (error) {
			console.error('Error fetching verses:', error);
			loading = false;
		}
	}

	function goBack() {
		goto('/');
	}
</script>

<section class="mt-8">
	{#if loading}
		<p>Loading...</p>
	{:else if surah}
		<div class="mt-8">
			<div
				class="fixed top-0 left-0 right-0 bg-base-300 py-4 z-10 shadow-md flex items-center justify-between px-20 max-sm:px-5"
			>
				<div>
					<h3 class="text-2xl font-bold mb-2 surahFont">
						{surah.name_simple} (Chapter {surah.id})
					</h3>
					<h4 class="text-xl font-bold surahFont text-gray-600">
						{surah.name_arabic}
					</h4>
				</div>
				<button class="btn btn-error mb-4 floating-button" on:click={goBack}>
					<i class="ri-arrow-go-back-line mr-2"></i>Go Back
				</button>
			</div>
			<div class="mt-24 surah-container">
				<ul class="list-decimal">
					{#each verses as verse}
						<li class="mb-2 mt-9">
							<p class="text-3xl text-right arabicFont">{verse.arabic}</p>
							<p class="mb-10 mt-9">{verse.english}</p>
							<div class="divider"></div>
						</li>
					{/each}
				</ul>
			</div>
		</div>
	{:else}
		<p>Surah not found.</p>
	{/if}
</section>
