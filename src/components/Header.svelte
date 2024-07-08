<script>
	import * as Dialog from '$lib/components/ui/dialog';
	import { Button, buttonVariants } from '$lib/components/ui/button/index.js';
	import { toggleMode } from 'mode-watcher';
	import * as Sheet from '$lib/components/ui/sheet';
</script>

<header class="gap-5 px-5 py-5 bg-base-300 border-b flex justify-between" id="header">
	<h1 class="text-3xl cursor-default font-serif max-md:text-2xl">Quranic</h1>
	<div class="lg:hidden">
		<Dialog.Root>
			<Dialog.Trigger class={buttonVariants({ variant: 'outline', size: 'icon' })}>
				<i class="ri-settings-3-line"></i>
			</Dialog.Trigger>
			<Dialog.Content class="sm:max-w-[425px]">
				<Dialog.Header>
					<Dialog.Title class="mb-3">Settings</Dialog.Title>
				</Dialog.Header>
				<h3 class="border-b">Theme</h3>
				<Button on:click={toggleMode} variant="outline">
					<p class="hidden transition-all dark:block">Light</p>
					<p class="transition-all dark:hidden">Dark</p>
					<span class="sr-only">Toggle theme</span>
				</Button>
				<h3 class="border-b mt-3">Bugs</h3>
				<a href="mailto:aliirtiza44@gmail.com"
					><Button variant="destructive">Found a bug? Report it here!</Button></a
				>
			</Dialog.Content>
		</Dialog.Root>
	</div>
	<div class="max-lg:hidden">
		<Sheet.Root>
			<Sheet.Trigger>
				<Button variant="outline" size="icon">
					<i class="ri-menu-fill"></i>
				</Button>
			</Sheet.Trigger>
			<Sheet.Content>
				<Sheet.Header>
					<Sheet.Title class="mb-3">Settings</Sheet.Title>
					<h3 class="border-b">Theme</h3>
					<Button on:click={toggleMode}>
						<p class="hidden transition-all dark:block">Light</p>
						<p class="transition-all dark:hidden">Dark</p>
						<span class="sr-only">Toggle theme</span>
					</Button>
					<h3 class="border-b mt-3">Bugs</h3>
					<a href="mailto:aliirtiza44@gmail.com"
						><Button variant="secondary">Found a bug? Report it here!</Button></a
					>
				</Sheet.Header>
				<Sheet.Footer>
					<Sheet.Close asChild let:builder>
						<Button builders={[builder]} variant="destructive">Close</Button>
					</Sheet.Close>
				</Sheet.Footer>
			</Sheet.Content>
		</Sheet.Root>
	</div>
</header>
