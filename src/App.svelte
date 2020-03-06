<script>
	import Header from './Header/Header.svelte'
	import Content from './Content/Content.svelte'
</script>

<main>
	<Header />
	<Content />
</main>

<style>
	:global(*) {
		margin: 0;
		padding: 0;
		color: slategray;
	}

	:global(button) {
		margin: 0;
		padding: 0;
	}

	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		font-family: 'Raleway'
	}
	
</style>