<script>
	import SurahInput from '../components/SurahInput.svelte';
	import Header from '../components/Header.svelte';
	import SurahList from '../components/SurahList.svelte';
	let searchQuery = '';

	function handleSearch(event) {
		searchQuery = event.detail.query;
		console.log('Updated search query in +page.svelte:', searchQuery);
	}
</script>

<Header></Header>
<SurahInput on:search={handleSearch}></SurahInput>
<SurahList {searchQuery}></SurahList>
