<script>
	function changeTheme(event) {
		const theme = event.target.value;
		document.documentElement.setAttribute('data-theme', theme);
		localStorage.setItem('selectedTheme', theme);
	}

	import { onMount } from 'svelte';
	import SecondaryHeader from '../../components/SecondaryHeader.svelte';
	onMount(() => {
		const storedTheme = localStorage.getItem('selectedTheme') || 'default';
		document.documentElement.setAttribute('data-theme', storedTheme);
		const themeButton = document.querySelector(`input[value="${storedTheme}"]`);
		if (themeButton) {
			themeButton.checked = true;
		}
	});
</script>

<SecondaryHeader></SecondaryHeader>
<div class="h-fit p-5 bg-base-100">
	<h1 class="text-7xl font-bold font-serif max-md:text-4xl max-sm:text-center">Settings</h1>
	<div class="divider"></div>
	<h1 class="text-3xl font max-sm:text-center"><i class="ri-palette-line mr-4"></i>Themes</h1>
	<div
		class="grid grid-cols-3 mt-5 gap-2 max-lg:grid-cols-2 max-sm:grid-cols-1 max-sm:place-items-center"
	>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Default"
				value="default"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Light"
				value="light"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="CupCake"
				value="cupcake"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Forest"
				value="forest"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Valentine"
				value="valentine"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Bumblebee"
				value="bumblebee"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Lofi"
				value="lofi"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Wireframe"
				value="wireframe"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Black"
				value="black"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Business"
				value="business"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Winter"
				value="winter"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Dim"
				value="dim"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Fantasy"
				value="fantasy"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Emerald"
				value="emerald"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Corporate"
				value="corporate"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide hover:shadow-lg"
				aria-label="Retro"
				value="retro"
				on:change={changeTheme}
			/>
		</div>
		<div class="w-fit h-fit">
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
	<div class="divider"></div>
	<h1 class="font text-3xl max-sm:text-center">
		<i class="ri-bug-2-line mr-4"></i>Report and Bugs
	</h1>
	<p class="mt-5 max-sm:text-center">
		Please note that this is the first release of the Quranic app, we're working hard to make your
		journey a memorable and fun.
		<br />
		If you see any anomaly or anything that is out of place, please let us know
		<a href="mailto:aliirtiza44@gmail.com" class="link">here.</a>
	</p>
	<div class="divider"></div>
	<h1 class="font text-3xl max-sm:text-center"><i class="ri-lightbulb-line mr-4"></i>Ideas</h1>
	<p class="mt-5 max-sm:text-center">
		Have you got a new idea that will help us make the journey better? What are you waiting for?
		Tell us! We love to hear your opinion and ideas!
	</p>
	<form action="https://formspree.io/f/mwkgdgql" method="POST">
		<div class="h-fit w-fit mt-5 mb-10 flex flex-col">
			<label class="input input-bordered flex items-center gap-2">
				Email
				<input type="email" class="grow" placeholder="abc@email.com" />
			</label>
			<textarea class="textarea textarea-bordered mt-3" placeholder="I would like a..."></textarea>
			<button type="submit" class="btn btn-primary mt-3 hover:shadow-lg"
				>Send<i class="ri-send-plane-2-line"></i>
			</button>
		</div>
	</form>
</div>
