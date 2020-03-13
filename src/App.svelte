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
	}

	:global(button) {
		margin: 0;
		padding: 0;
	}

	:global(h3) {
		margin-bottom: 20px;
	}
	
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		font-family: 'Raleway';
	}
	
</style>