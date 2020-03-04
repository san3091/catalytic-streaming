<script>
	import { onMount } from 'svelte'
	import queryString from 'query-string'
	
	// const CLIENT_ID = xxx
	// const CLIENT_SECRET = xxx
	const redirectURL = 'https://930b9287.ngrok.io'
	const patreonOAuthLink = `https://www.patreon.com/oauth2/authorize?response_type=code&client_id=${CLIENT_ID}&redirect_uri=${redirectURL}`

	onMount(async () => {
		const oauthGrantCode = queryString.parse(window.location.search).code
		const url = `https://www.patreon.com/api/oauth2/tokencode=${oauthGrantCode}&grant_type=authorization_code&client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}&redirect_uri=${redirectURL}`

		console.log(oauthGrantCode)
	})
</script>

<main>
	<a href={patreonOAuthLink}>login with patreon!</a>
</main>

<style>
</style>