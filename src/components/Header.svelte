<header class="navbar gap-5 px-5 py-5 bg-base-300 shadow-lg" id="header">
	<div class="navbar-start">
		<h1 class="text-3xl cursor-default font-serif max-md:text-2xl">Quranic</h1>
	</div>
	<div class="navbar-end">
		<div class="dropdown dropdown-end">
			<div tabindex="0" role="button" class="btn btn-outline">
				<i class="ri-menu-line"></i>
			</div>
			<!-- svelte-ignore a11y-no-noninteractive-tabindex -->
			<ul
				tabindex="0"
				class="dropdown-content z-[1] menu p-2 shadow-md bg-base-200 rounded-box w-52"
			>
				<li><a href="/"><i class="ri-home-line"></i>Home</a></li>
				<li><a href="#about"><i class="ri-question-line"></i>About Us</a></li>
				<li><a href="#updates"><i class="ri-refresh-line"></i>Updates</a></li>
				<li><a href="/player"><i class="ri-headphone-line"></i>Player</a></li>
				<li><a href="/settings"><i class="ri-settings-line"></i>Settings</a></li>
			</ul>
		</div>
	</div>
</header>
