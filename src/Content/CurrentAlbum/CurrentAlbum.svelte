<script>
  import SoundCloudPlayer from './SoundCloudPlayer/SoundCloudPlayer.svelte'
  import AlbumInfo from './AlbumInfo/AlbumInfo.svelte'

  export let selectedAlbum
  export let loading
  let albumInfo
</script>

<div class='current-album-container'>
  <div class='current-album'>
    <SoundCloudPlayer 
      selectedAlbum={selectedAlbum} 
      loading={loading}
    />
    <AlbumInfo album={selectedAlbum} />
  </div>
</div>

<style>
  .current-album-container {
    width: 100%;
    background-color: lavender;
    padding: 30px 0;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .current-album {
    display: flex;
    width: 1200px;
    flex-direction: row;
    justify-content: center;
  }
</style>