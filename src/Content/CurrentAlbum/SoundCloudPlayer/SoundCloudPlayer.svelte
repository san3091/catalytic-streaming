<script>
  import { onMount } from 'svelte'
  import { fade } from 'svelte/transition'

  export let selectedAlbumURL
  export let updateAlbumInfo
  export let setLoading
  let loading = false
  const mountPlayer = (url) => {
    loading = true
    setLoading(true)
    SC.oEmbed(url, {
      element: document.getElementById('sound-cloud')
    }).then((album) => {
      let iframe = document.getElementsByTagName('iframe')
      updateAlbumInfo(album)
      setLoading(false)
      loading = false
    })
  }

  $: mountPlayer(selectedAlbumURL)
  onMount(() => {   
    mountPlayer(selectedAlbumURL)
  })
</script>
  
<div class='player-container'>
  {#if loading}
    <div transition:fade class='loading'>
      <h1>Loading</h1>
    </div>
  {/if}
  <div id='sound-cloud'></div>
</div>

<style>
  .player-container {
    position: relative;
    width: 50%;
    height: 100%;
    background-color: white;
  }

  .loading {
    height: 100%;
    width: 100%;
    background-color: red;
    position: absolute;
    top: 0;
    left: 0;
  }
 
</style>
