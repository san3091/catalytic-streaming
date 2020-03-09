<script>
  import SoundCloudPlayer from './SoundCloudPlayer/SoundCloudPlayer.svelte'
  import AlbumInfo from './AlbumInfo/AlbumInfo.svelte'

  export let selectedAlbum
  let albumInfo
</script>

<div class='current-album'>
  <SoundCloudPlayer 
    selectedAlbum={selectedAlbum} 
  />
  <AlbumInfo album={selectedAlbum} />
</div>

<style>
  .current-album {
    display: flex;
    flex-direction: row;
    justify-content: center;
  }
</style>