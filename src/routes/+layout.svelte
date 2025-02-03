<script lang="ts">
	import '../app.css';
	import Navbar from '$lib/components/Navbar.svelte';
	let { children } = $props();
	import { onMount } from 'svelte';

	onMount(() => {
		const ga4Id = import.meta.env.VITE_GOOGLE_ANALYTICS_ID;

		if (!ga4Id) {
			console.error("GA4 ID is missing. Check your environment variables.");
			return;
		}

		if (!document.querySelector('script[src*="gtag/js"]')) {
			const script = document.createElement('script');
			script.async = true;
			script.src = `/gtag.js?id=${ga4Id}`;
			document.head.appendChild(script);

			script.onload = () => {
				window.dataLayer = window.dataLayer || [];
				// Define gtag *inside* onload, after dataLayer
				function gtag(){window.dataLayer.push(arguments);} // Access window.dataLayer

				gtag('js', new Date());
				gtag('config', ga4Id);

				gtag('event', 'page_view', {
					page_title: document.title,
					page_location: window.location.href,
				});
			};

			script.onerror = () => {
				console.error("Failed to load GA4 script.");
			};

		} else {
			console.warn("GA4 script already loaded. Skipping.");
		}
	});

</script>
<Navbar />
{@render children()}