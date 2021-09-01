<script>
	import Content from '../components/Content.svelte';
	import Footer from '../components/Footer.svelte';
	import Header from '../components/Header.svelte';
</script>

<svelte:head>
	<title>Less Code - Rahmat Agung Julians</title>
</svelte:head>

<div class="app">
	<Header />
	<main>
		<Content />
	</main>
	<Footer />
</div>

<style>
	.app {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
	}
	main {
		flex: 1;
	}
</style>
