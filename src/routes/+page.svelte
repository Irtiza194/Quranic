<script>
	import SurahInput from '../components/SurahInput.svelte';
	import Header from '../components/Header.svelte';
	import SurahList from '../components/SurahList.svelte';
	import About from '../components/About.svelte';
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
<button type="button" class="btn btn-primary mr-10 mb-10 float-end" on:click={goToTop}>
	<i class="ri-arrow-up-line"></i>
</button>
