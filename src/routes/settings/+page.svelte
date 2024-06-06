<script>
	import Header from '../../components/Header.svelte';
</script>

<Header></Header>
<div class="h-fit p-5 bg-base-100">
	<h1 class="text-7xl font-bold font-serif max-md:text-4xl">Settings</h1>
	<div class="divider"></div>
	<h1 class="text-3xl font">Themes</h1>
	<div
		class="grid grid-cols-3 mt-5 gap-2 max-lg:grid-cols-2 max-sm:grid-cols-1 max-md:items-center"
	>
		<div class="w-fit h-fit rounded" data-theme="default">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide rounded hover:shadow-lg"
				aria-label="Default"
				value="default"
			/>
		</div>
		<div class="w-fit h-fit rounded" data-theme="light">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide rounded hover:shadow-lg"
				aria-label="Light"
				value="light"
			/>
		</div>
		<div class="w-fit h-fit rounded" data-theme="cupcake">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide rounded hover:shadow-lg"
				aria-label="CupCake"
				value="cupcake"
			/>
		</div>
		<div class="w-fit h-fit rounded" data-theme="forest">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide rounded hover:shadow-lg"
				aria-label="Forest"
				value="forest"
			/>
		</div>
		<div class="w-fit h-fit rounded" data-theme="valentine">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide rounded hover:shadow-lg"
				aria-label="Valentine"
				value="valentine"
			/>
		</div>
		<div class="w-fit h-fit rounded" data-theme="bumblebee">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide rounded hover:shadow-lg"
				aria-label="Bumblebee"
				value="bumblebee"
			/>
		</div>
		<div class="w-fit h-fit rounded" data-theme="lofi">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide rounded hover:shadow-lg"
				aria-label="Lofi"
				value="lofi"
			/>
		</div>
		<div class="w-fit h-fit rounded" data-theme="luxury">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide rounded hover:shadow-lg"
				aria-label="Luxury"
				value="luxury"
			/>
		</div>
		<div class="w-fit h-fit rounded" data-theme="wireframe">
			<input
				type="radio"
				name="theme-buttons"
				class="btn theme-controller btn-wide rounded hover:shadow-lg"
				aria-label="Wireframe"
				value="wireframe"
			/>
		</div>
	</div>
	<p class="mt-5 text-error">
		Please note that the themes only work for this page at the moment, we're working hard to make
		your experience a memorable one.
	</p>
</div>
