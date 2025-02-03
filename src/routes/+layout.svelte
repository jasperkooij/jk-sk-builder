<script lang="ts">
	import { injectSpeedInsights } from '@vercel/speed-insights/sveltekit';
	import { browser } from '$app/environment';
	import { page } from '$app/stores';
	import '../app.css';

	const GA_MEASUREMENT_ID = import.meta.env.VITE_GOOGLE_ANALYTICS_ID;

	if (browser) {
		// Google Analytics script
		const gaScript = document.createElement('script');
		gaScript.src = `https://www.googletagmanager.com/gtag/js?id=${GA_MEASUREMENT_ID}`;
		gaScript.async = true;
		document.head.appendChild(gaScript);

		// Initialize gtag
		window.dataLayer = window.dataLayer || [];
		function gtag(...args: [string, Date | string, string?]): void {
			window.dataLayer.push(args);
		}
		gtag('js', new Date());
		gtag('config', GA_MEASUREMENT_ID);

		// Track page views
		page.subscribe((currentPage) => {
			gtag('event', 'page_view', {
				page_location: currentPage.url.href,
				page_path: currentPage.url.pathname,
				page_title: document.title
			});
		});
	}

	injectSpeedInsights();
	let { children } = $props();
</script>

{@render children()}