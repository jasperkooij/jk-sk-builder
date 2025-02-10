<script>
	let menuOpen = false;

	function toggleMenu() {
		menuOpen = !menuOpen;
	}

	function closeMenu() {
		menuOpen = false;
	}
</script>

<nav class="bg-base-200 p-4">
	<div class="container mx-auto flex items-center justify-between">
		<!-- Desktop Navbar -->
		<div class="hidden items-center space-x-6 md:flex">
			<img src="/logo.svg" alt="Logo" class="h-10" />
			<a href="/" class="btn btn-ghost">Home</a>
			<a href="/#about" class="btn btn-ghost">About</a>
			<a href="/blog" class="btn btn-ghost">Blog</a>
			<a href="/#contact" class="btn btn-ghost">Contact</a>
		</div>

		<!-- Mobile Navbar -->
		<div class="flex w-full items-center justify-between md:hidden">
			<div class="flex items-center space-x-4">
				<img src="/logo.svg" alt="Logo" class="h-8" />
				<a href="/" class="btn btn-ghost">Home</a>
			</div>
			<button class="btn btn-ghost text-xl" on:click={toggleMenu}> ☰ </button>
		</div>
	</div>

	<!-- Mobile Fullscreen Menu -->
	{#if menuOpen}
		<div
			class="bg-opacity-90 fixed inset-0 z-50 flex flex-col items-center justify-center space-y-6 bg-black text-lg text-white"
		>
			<button class="absolute top-5 right-5 text-3xl" on:click={closeMenu}>×</button>
			<img src="/logo.svg" alt="Logo" class="h-12" />
			<a href="/" class="btn btn-ghost text-2xl text-white" on:click={closeMenu}>Home</a>
			<a href="/#about" class="btn btn-ghost text-2xl text-white" on:click={closeMenu}>About</a>
			<a href="/blog" class="btn btn-ghost text-2xl text-white" on:click={closeMenu}>Blog</a>
			<a href="/#contact" class="btn btn-ghost text-2xl text-white" on:click={closeMenu}>Contact</a>
		</div>
	{/if}
</nav>
