<script>
  import Profile from './Profile/Profile.svelte'
</script>

<div class='header'>
  <div class='header-content'>
    <img src='/catalytic-sound-logo-(1)-WEB.png' alt='Catalytic Sound Logo' >
    <div class='header-right'>
      <Profile />
    </div>
  </div>
</div>

<style>
  .header {
    width: 100%;
    display: flex;
    justify-content: center;
  }

  .header-content {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 1200px;
  }

  img { 
    height: 60px;
  }
  .header-right {
    display: flex;
    flex-direction: row;
  }
</style>