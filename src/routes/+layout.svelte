<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/logos/logo.svg';
	import logo from '$lib/assets/logos/NFHS Hack club logo.png';


	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<meta property="og:image" content={logo} />
</svelte:head>

{@render children?.()}
