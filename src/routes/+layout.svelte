<script lang="ts">
	import { injectSpeedInsights } from '@vercel/speed-insights/sveltekit';
	import '../app.css';
	import { onMount } from 'svelte';
	import { page } from '$app/stores'; // Import page store at the top level
	injectSpeedInsights();
	let { children } = $props();
	let currentPage = null; // Initialize outside onMount, and assign in onMount
	let unsubscribe; // Store the unsubscribe function

	onMount(() => {
		// ... (GA4 script loading and gtag initialization - same as before)

		currentPage = $page; // Now assign the initial page value inside onMount

		unsubscribe = page.subscribe(new_page => {
			if (new_page.url !== currentPage?.url) { // Optional chaining for initial check
				gtag('event', 'page_view', {
					page_location: new_page.url.href,
					page_path: new_page.url.pathname,
					page_title: document.title
				});
				currentPage = new_page;
			}
		});

		return unsubscribe; // Important: Unsubscribe to prevent memory leaks!
	});

	// ... rest of your component code
</script>


{@render children()}
