<script>
  import { onMount } from 'svelte'
  import { fade } from 'svelte/transition'
  

  export let selectedAlbum
  export let loading
</script>
  
<div class='player-container'>
  {#if loading}
    <img transition:fade src='player-image.svg' />
  {:else}
    {@html selectedAlbum && selectedAlbum.html}
  {/if}
</div>

<style>
  .player-container {
    position: relative;
    width: 50%;
    height: 100%;
  }
  
  .player-loader {
    height: 450px;
    background-color: hsl(0, 0%, 100%, 80%);
    border: 3px dashed grey;
    margin: 5px;
  }

  .loader-image {
    height: 350px;
    border: 3px solid grey;
  }
  
  .play-icon {
    margin: 5px;
    height: 70px;
    width: 70px;
    border-radius: 50px;
    background-color: grey;
  }
</style>
