<script>
	import '../app.css';
	const title = 'Future Super | Cosgrove Solar Farm';
	const desc = 'Cosgrove Solar Farm';
	const image = 'https://www.futuresuper.com.au/images/future-super-og.png';
</script>

<svelte:head>
	<title>{title}</title>
	<meta charset="UTF-8" />
	<meta
		name="viewport"
		content="width=device-width, initial-scale=1.0 viewport-fit=cover"
		shrink-to-fit="no"
	/>
	<meta http-equiv="X-UA-Compatible" content="ie=edge" />
	<meta name="description" content={desc} />
	<meta property="og:title" content={title} />
	<meta property="og:description" content={desc} />
	<meta property="og:image" content={image} />
	<meta property="og:type" content="website" />
	<meta property="twitter:title" content={title} />
	<meta property="twitter:description" content={desc} />
	<meta property="twitter:image" content={image} />
	<meta name="twitter:card" content="summary_large_image" />
	<link
		rel="icon"
		type="image/png"
		sizes="32x32"
		href="https://www.futuresuper.com.au/images/favicon/favicon-32.png"
	/>
	<link
		rel="apple-touch-icon"
		href="https://www.futuresuper.com.au/images/favicon/apple-touch-icon.png"
	/>
	<link href="https://api.mapbox.com/mapbox-gl-js/v2.4.1/mapbox-gl.css" rel="stylesheet" />
</svelte:head>

<slot />
