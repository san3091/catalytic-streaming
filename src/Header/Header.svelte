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
    background-color: hsl(0, 0%, 100%, 80%);
  }

  .header-content {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 1200px;
  }

  img { 
    height: 60px;
    margin-left: -16px;
  }

  .header-right {
    display: flex;
    flex-direction: row;
  }
</style>