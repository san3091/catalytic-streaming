<script>
  import { onMount } from 'svelte'
  
  export let selectedAlbum
  export let loading

</script>
  
<div  class='player-container'>
  {#if loading}
    <!-- <img transition:fade src='player-image.svg' /> -->
  {:else}
    {@html selectedAlbum && selectedAlbum.html}
  {/if}
</div>

<style>
</style>
