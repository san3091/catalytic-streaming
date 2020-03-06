<script>
  import Search from './Search/Search.svelte'
  import Profile from './Profile/Profile.svelte'
</script>

<div class='header'>
  <div class='header-content'>
    <h1>Catalytic Sound Streaming</h1>
    <div class='header-right'>
      <Search />
      <Profile />
    </div>
  </div>
</div>

<style>
  .header {
    width: 100%;
    display: flex;
    justify-content: center;
    background-color: white;
  }

  .header-content {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 1200px;
  }

  .header-right {
    display: flex;
    flex-direction: row;
  }
</style>