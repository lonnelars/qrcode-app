<script>
	import QRCode from 'qrcode';

	let text = 'https://www.kantega.no/';
	$: dataURLPromise = QRCode.toDataURL(text, { type: 'image/png', margin: 0, width: 800 });

	function downloadName(text) {
		const url = makeURL(text);
		if (url) {
			return url.host + '.png';
		} else {
			return 'qrcode.png';
		}
	}

	function makeURL(s) {
		try {
			return new URL(s);
		} catch (error) {
			return null;
		}
	}
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
	{#await dataURLPromise then dataURL}
		<p>
			<a href={dataURL} download={downloadName(text)}>Last ned QR-koden</a>
		</p>
		<img src={dataURL} title={`qrcode-${text}.png`} alt={`En QR-kode av teksten "${text}"`} />
	{/await}
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

	h1,
	p {
		margin: 0;
	}

	.input {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;

		& input {
			font-size: 1.5rem;
			padding: 1rem 0.5rem;
			border-radius: 10px;
			border: 2px solid;
		}
	}

	img {
		width: 100%;
		display: block;
	}
</style>
