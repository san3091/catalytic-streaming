<script>
  import AlbumInfo from './AlbumInfo/AlbumInfo.svelte'

  import { onMount } from 'svelte'
  export let selectedAlbumURL

  let albumInfo
  const mountPlayer = (url) => {
    SC.oEmbed(url, {
      element: document.getElementById('sound-cloud')
    }).then((album) => {
      albumInfo = album
      console.log(album)
    })
  }

  $: mountPlayer(selectedAlbumURL)
  onMount(() => {   
    mountPlayer(selectedAlbumURL)
  })
</script>

<div class='current-album'>
  <div id='sound-cloud'>something</div>
  <AlbumInfo albumInfo={albumInfo}/>
</div>

<style>
  .current-album {
    display: flex;
    flex-direction: row;
    width: 100%;
  }

  #sound-cloud {
    width: 60%;
    flex-grow: 2;
  }
</style>