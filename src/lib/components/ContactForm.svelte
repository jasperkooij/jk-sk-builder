<!-- src/components/ContactForm.svelte -->
<script>
	let formData = {
		name: '',
		email: '',
		message: ''
	};

	let successMessage = '';
	let errorMessage = '';

	async function handleSubmit(event) {
		event.preventDefault();

		const response = await fetch('https://formspree.io/f/myyvpapn', {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify(formData)
		});

		if (response.ok) {
			successMessage = 'Your message has been sent successfully!';
			errorMessage = '';
			formData = { name: '', email: '', message: '' }; // Reset form
		} else {
			errorMessage = 'There was an error sending your message. Please try again.';
			successMessage = '';
		}
	}
</script>

<div class="mx-auto max-w-md">
	<form on:submit|preventDefault={handleSubmit} class="card bg-base-100 p-6 shadow-xl">
		<h2 class="mb-4 text-2xl font-bold">Contact Us</h2>

		<!-- Success Message -->
		{#if successMessage}
			<div class="alert alert-success">
				<span>{successMessage}</span>
			</div>
		{/if}

		<!-- Error Message -->
		{#if errorMessage}
			<div class="alert alert-error">
				<span>{errorMessage}</span>
			</div>
		{/if}

		<!-- Name Field -->
		<div class="mb-4 grid grid-cols-1 items-center gap-4 md:grid-cols-[1fr_2fr]">
			<label class="label justify-start" for="name">
				<span class="label-text">Name</span>
			</label>
			<input
				type="text"
				id="name"
				placeholder="Your Name"
				class="input input-bordered w-full"
				bind:value={formData.name}
				required
			/>
		</div>

		<!-- Email Field -->
		<div class="mb-4 grid grid-cols-1 items-center gap-4 md:grid-cols-[1fr_2fr]">
			<label class="label justify-start" for="email">
				<span class="label-text">Email</span>
			</label>
			<input
				type="email"
				id="email"
				placeholder="Your Email"
				class="input input-bordered w-full"
				bind:value={formData.email}
				required
			/>
		</div>

		<!-- Message Field -->
		<div class="mb-4 grid grid-cols-1 items-start gap-4 md:grid-cols-[1fr_2fr]">
			<label class="label justify-start" for="message">
				<span class="label-text">Message</span>
			</label>
			<textarea
				id="message"
				placeholder="Your Message"
				class="textarea textarea-bordered h-24 w-full"
				bind:value={formData.message}
				required
			></textarea>
		</div>

		<!-- Submit Button -->
		<button type="submit" class="btn btn-primary mt-6 w-full">Send Message</button>
	</form>
</div>
