<script>
	import QRCode from 'qrcode';

	let text = 'https://www.kantega.no/';
	$: promise = QRCode.toString(text, { type: 'svg', margin: 0 }).then((svgString) =>
		URL.createObjectURL(new Blob([svgString], { type: 'image/svg+xml' }))
	);
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="QR codes" />
</svelte:head>

<section>
	<h1>Lag QR-kode av en URL</h1>
	<div class="input">
		<label for="input">Skriv inn URL:</label>
		<input type="text" id="input" bind:value={text} />
	</div>
	<div id="svg">
		{#await promise then dataURL}
			<img src={dataURL} alt={`En QR-kode av teksten "${text}"`} />
		{/await}
	</div>
</section>

<style>
	section {
		max-width: 800px;
		font-family: 'Source Sans Pro', Arial, sans-serif;
		font-size: 1.5rem;

		display: flex;
		flex-direction: column;
		gap: 2rem;
	}

	h1 {
		margin: 0;
	}

	.input {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;

		& input {
			font-size: 1.5rem;
			padding: 1rem .5rem;
			border-radius: 10px;
			border: 2px solid

		}
	}
</style>
