<script>
  import SoundCloudPlayer from './SoundCloudPlayer/SoundCloudPlayer.svelte'
  import AlbumInfo from './AlbumInfo/AlbumInfo.svelte'

  export let selectedAlbumURL
  let loading = true
  let albumInfo
  const setLoading = (bool) => {
    loading = bool
  }

  const updateAlbumInfo = (newInfo) => {
    albumInfo = newInfo
  }
</script>

<div class='current-album'>
  <SoundCloudPlayer 
    setLoading={setLoading}
    selectedAlbumURL={selectedAlbumURL} 
    updateAlbumInfo={updateAlbumInfo} />
  <AlbumInfo albumInfo={albumInfo} loading={loading} />
</div>

<style>
  .current-album {
    display: flex;
    flex-direction: row;
    justify-content: center;
  }
</style>