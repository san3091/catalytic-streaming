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
    width: 100%;
    height: 100%;
  }
</style>
