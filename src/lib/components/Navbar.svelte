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
	<div class="container mx-auto flex justify-between items-center">
		<!-- Desktop Navbar -->
		<div class="hidden md:flex items-center space-x-6">
			<img src="/logo.svg" alt="Logo" class="h-10" />
			<a href="/" class="btn btn-ghost">Home</a>
			<a href="/#about" class="btn btn-ghost">About</a>
			<a href="/blog" class="btn btn-ghost">Blog</a>
			<a href="/#contact" class="btn btn-ghost">Contact</a>
		</div>

		<!-- Mobile Navbar -->
		<div class="flex md:hidden w-full justify-between items-center">
			<div class="flex items-center space-x-4">
				<img src="/logo.svg" alt="Logo" class="h-8" />
				<a href="/" class="btn btn-ghost">Home</a>
			</div>
			<button class="btn btn-ghost text-xl" on:click={toggleMenu}>
				☰
			</button>
		</div>
	</div>

	<!-- Mobile Fullscreen Menu -->
	{#if menuOpen}
		<div class="fixed inset-0 bg-black bg-opacity-90 flex flex-col items-center justify-center space-y-6 text-white text-lg z-50">
			<button class="absolute top-5 right-5 text-3xl" on:click={closeMenu}>×</button>
			<img src="/logo.svg" alt="Logo" class="h-12" />
			<a href="/" class="btn btn-ghost text-white text-2xl" on:click={closeMenu}>Home</a>
			<a href="/#about" class="btn btn-ghost text-white text-2xl" on:click={closeMenu}>About</a>
			<a href="/blog" class="btn btn-ghost text-white text-2xl" on:click={closeMenu}>Blog</a>
			<a href="/#contact" class="btn btn-ghost text-white text-2xl" on:click={closeMenu}>Contact</a>
		</div>
	{/if}
</nav>
