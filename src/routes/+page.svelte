<script>
	import SurahInput from '../components/SurahInput.svelte';
	import Header from '../components/Header.svelte';
	import SurahList from '../components/SurahList.svelte';
	import About from '../components/About.svelte';
	import { Button } from '$lib/components/ui/button/index.js';
	let searchQuery = '';

	function handleSearch(event) {
		searchQuery = event.detail.query;
		console.log('Updated search query in +page.svelte:', searchQuery);
	}
	function goToTop() {
		location.href = '#header';
	}
</script>

<Header></Header>
<SurahInput on:search={handleSearch}></SurahInput>
<SurahList {searchQuery}></SurahList>
<About></About>
<Button variant="outline" size="icon" class="float-end mb-10 mr-10" on:click={goToTop}>
	<i class="ri-arrow-up-line"></i>
</Button>
