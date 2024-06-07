<script>
	import '../app.css';
	import { onMount } from 'svelte';

	onMount(() => {
		const storedTheme = localStorage.getItem('selectedTheme') || 'default';
		document.documentElement.setAttribute('data-theme', storedTheme);
	});
</script>

<slot />
