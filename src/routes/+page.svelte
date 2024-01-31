<script>
	import QRCode from 'qrcode';

	let text = 'https://www.kantega.no/';
	$: promise = QRCode.toString(text, { type: 'svg' });
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="QR codes" />
</svelte:head>

<section>
	<h1>Lag QR-kode av en URL</h1>
	<label for="input">Skriv inn URL:</label>
	<input type="text" id="input" bind:value={text} />
	<div id="svg">{#await promise then svg}{@html svg}{/await}</div>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		max-width: 800px;
	}

	#svg {
		width: 600px;
		height: 600px;
	}
</style>
