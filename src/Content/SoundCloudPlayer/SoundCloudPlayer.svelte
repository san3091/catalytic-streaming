<script>
  import AlbumInfo from './AlbumInfo/AlbumInfo.svelte'

  import { onMount } from 'svelte'
  export let selectedAlbumURL

  let albumInfo
  const mountPlayer = (url) => {
    SC.oEmbed(url, {
      element: document.getElementById('sound-cloud')
    }).then((album) => {
      let iframe = document.getElementsByTagName('iframe')
      albumInfo = album
    })
  }

  $: mountPlayer(selectedAlbumURL)
  onMount(() => {   
    mountPlayer(selectedAlbumURL)
  })
</script>

<div class='current-album'>
  <div id='sound-cloud'></div>
  <AlbumInfo albumInfo={albumInfo}/>
</div>

<style>
  .current-album {
    display: flex;
    flex-direction: row;
    justify-content: center;
  }

  #sound-cloud {
    width: 50%;
  }
</style>