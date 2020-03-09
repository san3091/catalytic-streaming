<script>
  import { onMount } from 'svelte'
  import { fade } from 'svelte/transition'

  export let selectedAlbum
</script>
  
<div class='player-container'>
  {@html selectedAlbum && selectedAlbum.html}
</div>

<style>
  .player-container {
    position: relative;
    width: 50%;
    height: 100%;
    background-color: white;
  }
</style>
