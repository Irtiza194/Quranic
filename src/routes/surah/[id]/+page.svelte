<script>
	import { onMount } from 'svelte';
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';
	import { get } from 'svelte/store';

	let surahId;
	let surah = null;
	let verses = [];
	let loading = false;

	$: surahId = get(page).params.id;

	onMount(() => {
		fetchSurahData(surahId);

		page.subscribe((value) => {
			if (value.params.id !== surahId) {
				surahId = value.params.id;
				fetchSurahData(surahId);
			}
		});
	});

	async function fetchSurahData(id) {
		try {
			loading = true;
			const response = await fetch(`https://api.quran.com/api/v4/chapters/${id}`);
			const data = await response.json();
			surah = data.chapter;
			await fetchVerses(id);
		} catch (error) {
			console.error('Error fetching surah data:', error);
		} finally {
			loading = false;
		}
	}

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
		} catch (error) {
			console.error('Error fetching verses:', error);
		} finally {
			loading = false;
		}
	}

	function goBack() {
		goto('/');
	}

	function goToNextSurah() {
		const nextSurahId = parseInt(surahId) + 1;
		goto(`/surah/${nextSurahId}`);
	}

	function goToPreviousSurah() {
		const prevSurahId = parseInt(surahId) - 1;
		goto(`/surah/${prevSurahId}`);
	}
</script>

<section class="mt-8">
	{#if loading}
		<div class="flex justify-center items-center h-screen flex-col">
			<span class="loading loading-spinner loading-md"></span>
			<h1 class="mt-3">Loading, please wait...</h1>
		</div>
	{:else if surah}
		<div class="mt-8">
			<div
				class="fixed max-md:text-center top-0 left-0 right-0 bg-base-300 py-4 z-10 shadow-md flex flex-col md:flex-row items-center justify-between px-4 md:px-20"
			>
				<div>
					<h3 class="text-2xl font-bold mb-2 surahFont">
						{surah.name_simple} (Chapter {surah.id})
					</h3>
					<h4 class="text-xl font-bold surahFont text-gray-600">
						{surah.name_arabic}
					</h4>
					<p class="text-lg text-gray-500">{surah.translated_name.name}</p>
				</div>
				<div class="flex space-x-2 max-md:mt-3 md:space-x-4">
					<button
						class="btn btn-primary hover:shadow-2xl mb-4"
						on:click={goToPreviousSurah}
						disabled={surah.id == 1}
					>
						<i class="ri-arrow-left-line mr-1"></i>
						<span class="hidden md:inline">Previous Surah</span>
					</button>
					<button class="btn btn-primary hover:shadow-2xl mb-4" on:click={goToNextSurah}>
						<span class="hidden md:inline">Next Surah</span>
						<i class="ri-arrow-right-line ml-1"></i>
					</button>
					<button class="btn btn-error mb-4 hover:shadow-2xl" on:click={goBack}>
						<i class="ri-arrow-go-back-line mr-1"></i>
						<span class="hidden md:inline">Go Back</span>
					</button>
				</div>
			</div>
			<div class="surah-container">
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
