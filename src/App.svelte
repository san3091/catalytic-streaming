<script>
	import Banner from './Banner/Banner.svelte'
	import Main from './Main/Main.svelte'
</script>

<main>
	<Banner />
	<Main />
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
</style>