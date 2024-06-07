<script>
	import '../app.css';
<<<<<<< HEAD
	import { onMount } from 'svelte';

	onMount(() => {
		const storedTheme = localStorage.getItem('selectedTheme') || 'default';
		document.documentElement.setAttribute('data-theme', storedTheme);
	});
=======
>>>>>>> 8dee79318e5264ba3b64ade30074ee9cd41b09b7
</script>

<slot />
