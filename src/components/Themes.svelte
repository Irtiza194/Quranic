<script>
	import { onMount } from 'svelte';

	function changeTheme(event) {
		const theme = event.target.value;
		document.documentElement.setAttribute('data-theme', theme);
		localStorage.setItem('selectedTheme', theme);
	}
	onMount(() => {
		const storedTheme = localStorage.getItem('selectedTheme') || 'default';
		document.documentElement.setAttribute('data-theme', storedTheme);
		const themeButton = document.querySelector(`input[value="${storedTheme}"]`);
		if (themeButton) {
			themeButton.checked = true;
		}
	});
</script>

<h1 class="text-7xl font-bold font-serif max-md:text-4xl max-sm:text-center">Settings</h1>
<div class="divider"></div>
<h1 class="text-3xl font max-sm:text-center"><i class="ri-color-filter-line mr-4"></i>Themes</h1>
<div class="grid grid-cols-[repeat(auto-fill,minmax(16rem,1fr))] mt-5 gap-2">
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Default"
			value="default"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Dark"
			value="dark"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Light"
			value="light"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="CupCake"
			value="cupcake"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="CyberPunk"
			value="cyberpunk"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Forest"
			value="forest"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Valentine"
			value="valentine"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Bumblebee"
			value="bumblebee"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Lofi"
			value="lofi"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Wireframe"
			value="wireframe"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Black"
			value="black"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Business"
			value="business"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Winter"
			value="winter"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Dim"
			value="dim"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Fantasy"
			value="fantasy"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Emerald"
			value="emerald"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Corporate"
			value="corporate"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Retro"
			value="retro"
			on:change={changeTheme}
		/>
	</div>
	<div class="">
		<input
			type="radio"
			name="theme-buttons"
			class="btn theme-controller btn-wide hover:shadow-lg"
			aria-label="Pastel"
			value="pastel"
			on:change={changeTheme}
		/>
	</div>
</div>
