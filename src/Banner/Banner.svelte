<script>
  import Search from './Search/Search.svelte'
  import Profile from './Profile/Profile.svelte'
</script>

<div class='banner'>
	<h1>Catalytic Sound Streaming</h1>
  <div class='banner-right'>
    <Search />
    <Profile />
  </div>
</div>

<style>
  .banner {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }

  .banner-right {
    display: flex;
    flex-direction: row;
  }
</style>