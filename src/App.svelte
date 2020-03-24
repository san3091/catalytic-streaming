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
		color: #3e3e3e;
	}

	:global(button) {
		margin: 0;
		padding: 0;
	}

	:global(h2) {
		margin: 30px 0 15px;
	}

	:global(body) {
		background-color: #DBDEDF;
		padding: 0px;
	}
	
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		font-family: 'Raleway';
	}
</style>